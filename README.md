# HHP 前端

Vue 3 + Vite + Element Plus。所有接口请求使用 **`/api` 前缀**，由 Nginx（生产）或 Vite 开发代理转发到 Flask（`127.0.0.1:5001`）。

## 本地开发

```bash
cd template
npm install
cp .env.example .env.development   # 默认 http://127.0.0.1:5001
# 另开终端启动后端
cd ../backend && python3 main.py
npm run dev
```

浏览器访问 `http://localhost:5173`，接口直连 `http://127.0.0.1:5001`（需后端已启动，且 Flask 已开启 CORS）。

## 生产构建

```bash
cp .env.production.example .env.production   # VITE_API_BASE_URL=/api
npm run build
```

产物在 `dist/`。

## 服务器部署

### 1. 上传静态资源

```bash
rsync -avz dist/ user@服务器:/var/www/hhp/web/
```

### 2. Nginx 配置（前端 + API 反代）

```nginx
server {
    listen 80;
    server_name yourdomain.com;
    root /var/www/hhp/web;
    index index.html;

    # 前端 SPA
    location / {
        try_files $uri $uri/ /index.html;
    }

    # API：/api/login -> http://127.0.0.1:5001/login
    location /api/ {
        proxy_pass http://127.0.0.1:5001/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        client_max_body_size 20m;
    }
}
```

### 3. 启动后端

```bash
cd /var/www/hhp/backend
source .venv/bin/activate
gunicorn -w 4 -b 127.0.0.1:5001 main:app --timeout 120
```

### 4. 验证

```bash
curl -X POST http://yourdomain.com/api/login \
  -H "Content-Type: application/json" \
  -d '{"account":"账号","password":"密码"}'
```

## 环境变量

| 环境 | 文件 | `VITE_API_BASE_URL` |
|------|------|---------------------|
| 开发 `npm run dev` | `.env.development` | `http://127.0.0.1:5001` |
| 生产 `npm run build` | `.env.production` | `/api`（Nginx 反代） |

修改环境变量后需重新执行 `npm run dev` 或 `npm run build`。




常用 Git 操作
1. 查看当前状态
git status
2. 添加文件到暂存区
git add .          # 添加所有文件
git add 文件名      # 添加指定文件
3. 提交代码
git commit -m "提交说明"
4. 推送到 GitHub
git push origin main    # 推送到 main 分支
5. 从 GitHub 拉取更新
git pull origin main



# 1. 切到目标分支 main
git switch main

# 2. 拉取 main 最新代码
git pull

# 3. 合并功能分支
git merge feature/login

# 4. 推送到远程
git push


git fetch origin
git switch feature/login
git rebase origin/main


1. 创建新分支前：要先更新 main
这是对的，因为新分支最好基于最新的 main。

bash
git status              # 确保工作区干净
git switch main
git pull                # 或 git pull --rebase
git switch -c feature/xxx
这样新分支就是从最新 main 开始的，后面冲突会少很多。

2. 切换到已有分支：拉取该分支，不是先拉 main
比如你要继续开发 feature/login：

bash
git status
git fetch origin
git switch feature/login
git pull
这里 git pull 拉的是 feature/login 的远程更新，不是 main。

如果你先切到 main 拉取，再切回 feature/login，这个功能分支本身可能还是旧的，远程别人推的代码你并没有拉下来。

3. 如果你想让功能分支同步 main 最新代码
不是“切换分支前先拉 main”，而是切到功能分支后，把 main 合并或 rebase 进来：

bash
git fetch origin
git switch feature/login
git rebase origin/main
或者：

bash
git merge origin/main
rebase 历史更线性，但如果是多人共用的分支，不要随便 rebase，用 merge 更安全。

4. 推荐日常流程
开始新功能
bash
git status
git switch main
git pull --rebase
git switch -c feature/xxx
继续已有功能
bash
git status
git fetch origin
git switch feature/xxx
git pull --rebase
功能分支同步 main
bash
git fetch origin
git switch feature/xxx
git rebase origin/main
