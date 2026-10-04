<script setup>
import { ref } from 'vue'

// 语言切换 (EN/CN)
const currentLang = ref('en')

// 语言切换
function toggleLang() {
  currentLang.value = currentLang.value === 'en' ? 'cn' : 'en'
}

// 表单数据
const formData = ref({
  mpn: '',
  manufacturer: '',
  quantity: '',
  email: '',
  notes: ''
})

const formStatus = ref('')

// 导航菜单
const navItems = [
  { id: 'global-sourcing', labelEn: 'Global Sourcing', labelCn: '全球采购', href: '#global-sourcing' },
  { id: 'ortaklar', labelEn: 'Our Partners', labelCn: '合作伙伴', href: '#ortaklar' },
  { id: 'is-gelistirme', labelEn: 'Business Development', labelCn: '业务发展', href: '#is-gelistirme' },
  { id: 'danismanlik', labelEn: 'Consulting', labelCn: '咨询服务', href: '#danismanlik' },
  { id: 'hakkimizda', labelEn: 'About Us', labelCn: '关于我们', href: '#hakkimizda' },
  { id: 'iletisim', labelEn: 'Contact', labelCn: '联系我们', href: '#iletisim' }
]

// 合作伙伴
const partners = [
  {
    index: '01',
    name: 'WINSOURCE',
    roleEn: 'AUTHORIZED PARTNER',
    roleCn: '授权合作伙伴',
    descEn: 'Global electronic component sourcing solutions.',
    descCn: '全球电子元器件采购解决方案。'
  },
  {
    index: '02',
    name: 'MEISHUO',
    isCyan: true,
    roleEn: 'AUTHORIZED REPRESENTATIVE',
    roleCn: '授权代表',
    descEn: 'Electromechanical products and Turkey market development.',
    descCn: '机电产品和土耳其市场开发。'
  }
]

// Sourcing 特性
const sourcingFeatures = [
  { labelEn: 'Global Network', labelCn: '全球网络' },
  { labelEn: 'Hard-to-Find', labelCn: '稀缺物料' },
  { labelEn: 'Long Lead Time', labelCn: '长交期物料' },
  { labelEn: 'Commercial Support', labelCn: '商务支持' }
]

// Bizdev 能力
const capabilities = [
  { labelEn: 'Market analysis and strategy', labelCn: '市场分析与战略' },
  { labelEn: 'Distributor and channel management', labelCn: '经销商与渠道管理' },
  { labelEn: 'OEM / EMS and industrial customer access', labelCn: 'OEM/EMS及工业客户对接' },
  { labelEn: 'Long-term business partnerships', labelCn: '长期商业合作' }
]

// 表单提交
function handleSubmit() {
  if (!formData.value.mpn || !formData.value.email) {
    formStatus.value = currentLang.value === 'en' ? 'Please fill in required fields.' : '请填写必填项。'
    return
  }
  formStatus.value = currentLang.value === 'en' ? 'Submitting...' : '提交中...'
  setTimeout(() => {
    formStatus.value = currentLang.value === 'en' 
      ? 'RFQ submitted successfully! We will contact you soon.' 
      : 'RFQ 提交成功！我们将尽快与您联系。'
    formData.value = { mpn: '', manufacturer: '', quantity: '', email: '', notes: '' }
  }, 1000)
}

// WhatsApp
function openWhatsApp() {
  window.open('https://wa.me/yourphonenumber', '_blank')
}
</script>

<template>
  <div class="page-wrapper">
    <!-- ================= NAV ================= -->
    <header class="site-header">
      <div class="container header-inner">
        <a href="#top" class="brand">
          <span class="brand-mark">
            <svg width="32" height="32" viewBox="0 0 32 32" fill="none">
              <path d="M16 2L30 24H2L16 2Z" stroke="currentColor" stroke-width="2" stroke-linejoin="round"/>
              <path d="M16 12L22 22H10L16 12Z" fill="currentColor"/>
            </svg>
          </span>
          <span class="brand-word">ASTRA<em>TECHNIC</em></span>
        </a>

        <nav class="primary-nav">
          <ul>
            <li v-for="item in navItems" :key="item.id">
              <a :href="item.href">
                {{ currentLang === 'en' ? item.labelEn : item.labelCn }}
              </a>
            </li>
          </ul>
        </nav>

        <div class="header-actions">
          <button class="lang-switch" type="button" @click="toggleLang">
            <span :class="{ 'is-active': currentLang === 'en' }">EN</span>
            <span class="lang-sep">/</span>
            <span :class="{ 'is-active': currentLang === 'cn' }">中文</span>
          </button>
          <a href="#iletisim" class="btn btn-primary">
            {{ currentLang === 'en' ? 'SEND RFQ' : '提交询价' }}
          </a>
          <button class="nav-toggle" type="button" aria-label="Menu">
            <span></span><span></span><span></span>
          </button>
        </div>
      </div>
    </header>

    <main id="main">
      <!-- ================= HERO ================= -->
      <section class="hero" id="top">
        <div class="hero-bg">
          <div class="hero-gradient"></div>
          <div class="hero-grid"></div>
          <div class="hero-glow hero-glow-1"></div>
          <div class="hero-glow hero-glow-2"></div>
        </div>

        <div class="container hero-content">
          <div class="hero-text">
            <div class="hero-badge">
              <span class="badge-dot"></span>
              <span>{{ currentLang === 'en' ? 'Trusted by Global Brands' : '深受全球品牌信赖' }}</span>
            </div>
            <h1 class="hero-title">
              {{ currentLang === 'en' ? 'Technology,' : '科技,' }}
              <span class="gradient-text">{{ currentLang === 'en' ? 'meets the right' : '汇聚于正确' }}</span>
              <br>{{ currentLang === 'en' ? 'parts.' : '的元器件.' }}
            </h1>
            <p class="hero-description">
              {{ currentLang === 'en' 
                ? 'We connect global manufacturers, supply sources, and technology companies with the right business opportunities.'
                : '我们致力于将全球制造商、供应商和科技公司与正确的商业机会连接起来。'
              }}
            </p>
            <div class="hero-stats">
              <div class="stat-item">
                <span class="stat-number">500+</span>
                <span class="stat-label">{{ currentLang === 'en' ? 'Global Partners' : '全球合作伙伴' }}</span>
              </div>
              <div class="stat-divider"></div>
              <div class="stat-item">
                <span class="stat-number">10K+</span>
                <span class="stat-label">{{ currentLang === 'en' ? 'Components Sourced' : '已采购元器件' }}</span>
              </div>
              <div class="stat-divider"></div>
              <div class="stat-item">
                <span class="stat-number">15+</span>
                <span class="stat-label">{{ currentLang === 'en' ? 'Years Experience' : '年行业经验' }}</span>
              </div>
            </div>
            <div class="hero-actions">
              <a href="#iletisim" class="btn btn-primary btn-lg">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M22 2L11 13M22 2l-7 20-4-9-9-4 20-7z"/>
                </svg>
                {{ currentLang === 'en' ? 'SEND RFQ' : '提交询价' }}
              </a>
              <a href="#hakkimizda" class="btn btn-outline">
                {{ currentLang === 'en' ? 'Learn More' : '了解更多' }}
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M5 12h14M12 5l7 7-7 7"/>
                </svg>
              </a>
            </div>
          </div>
          <div class="hero-visual">
            <div class="visual-card visual-card-1">
              <div class="card-icon">
                <svg width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
                  <circle cx="12" cy="12" r="10"/>
                  <path d="M2 12h20M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z"/>
                </svg>
              </div>
              <span>{{ currentLang === 'en' ? 'Global Network' : '全球网络' }}</span>
            </div>
            <div class="visual-card visual-card-2">
              <div class="card-icon">
                <svg width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
                  <path d="M21 16V8a2 2 0 0 0-1-1.73l-7-4a2 2 0 0 0-2 0l-7 4A2 2 0 0 0 3 8v8a2 2 0 0 0 1 1.73l7 4a2 2 0 0 0 2 0l7-4A2 2 0 0 0 21 16z"/>
                  <polyline points="3.27 6.96 12 12.01 20.73 6.96"/>
                  <line x1="12" y1="22.08" x2="12" y2="12"/>
                </svg>
              </div>
              <span>{{ currentLang === 'en' ? 'Supply Chain' : '供应链' }}</span>
            </div>
            <div class="visual-card visual-card-3">
              <div class="card-icon">
                <svg width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
                  <path d="M12 2L2 7l10 5 10-5-10-5z"/>
                  <path d="M2 17l10 5 10-5"/>
                  <path d="M2 12l10 5 10-5"/>
                </svg>
              </div>
              <span>{{ currentLang === 'en' ? 'Components' : '元器件' }}</span>
            </div>
          </div>
        </div>

        <div class="scroll-indicator">
          <span>{{ currentLang === 'en' ? 'Scroll' : '滚动' }}</span>
          <div class="scroll-mouse">
            <div class="scroll-wheel"></div>
          </div>
        </div>
      </section>

      <!-- ================= SERVICES ================= -->
      <section class="services" id="global-sourcing">
        <div class="container">
          <div class="section-header">
            <span class="section-label">{{ currentLang === 'en' ? 'OUR SERVICES' : '我们的服务' }}</span>
            <h2 class="section-title">
              {{ currentLang === 'en' ? 'Comprehensive Electronic' : '全面的电子元器件' }}
              <span class="gradient-text">{{ currentLang === 'en' ? 'Component Solutions' : '解决方案' }}</span>
            </h2>
          </div>

          <div class="services-grid">
            <div class="service-card service-card-main">
              <div class="service-icon">
                <svg width="40" height="40" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
                  <circle cx="12" cy="12" r="10"/>
                  <path d="M2 12h20M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z"/>
                </svg>
              </div>
              <h3>{{ currentLang === 'en' ? 'Global Sourcing' : '全球采购' }}</h3>
              <p>
                {{ currentLang === 'en'
                  ? 'As a Winsource Authorized Partner, we provide global sourcing support for your active, long-term, hard-to-find, and specific electronic component needs.'
                  : '作为 Winsource 授权合作伙伴，我们为您的活跃、长期、稀缺及特定电子元器件需求提供全球采购支持。'
                }}
              </p>
              <ul class="feature-list">
                <li v-for="feature in sourcingFeatures" :key="feature.labelEn">
                  <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <polyline points="20 6 9 17 4 12"/>
                  </svg>
                  {{ currentLang === 'en' ? feature.labelEn : feature.labelCn }}
                </li>
              </ul>
              <a href="#iletisim" class="service-link">
                {{ currentLang === 'en' ? 'Request Quote' : '获取报价' }}
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M5 12h14M12 5l7 7-7 7"/>
                </svg>
              </a>
            </div>

            <div class="service-card">
              <div class="service-icon">
                <svg width="40" height="40" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
                  <path d="M16 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"/>
                  <circle cx="8.5" cy="7" r="4"/>
                  <path d="M20 8v6M23 11h-6"/>
                </svg>
              </div>
              <h3>{{ currentLang === 'en' ? 'Business Development' : '业务发展' }}</h3>
              <p>
                {{ currentLang === 'en'
                  ? 'We create sales representation, channel development, customer access, and long-term business partnerships for global manufacturers.'
                  : '我们为全球制造商提供销售代理、渠道开发、客户对接和长期商业合作服务。'
                }}
              </p>
            </div>

            <div class="service-card">
              <div class="service-icon">
                <svg width="40" height="40" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
                  <path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/>
                </svg>
              </div>
              <h3>{{ currentLang === 'en' ? 'Consulting' : '咨询服务' }}</h3>
              <p>
                {{ currentLang === 'en'
                  ? 'We transfer our technical and commercial experience in the electronic component ecosystem to market development and project-based consulting.'
                  : '我们将电子元器件领域的专业经验转化为市场开发和项目咨询服务。'
                }}
              </p>
            </div>
          </div>
        </div>
      </section>

      <!-- ================= PARTNERS ================= -->
      <section class="partners" id="ortaklar">
        <div class="partners-bg">
          <div class="partners-pattern"></div>
        </div>
        <div class="container">
          <div class="section-header section-header-light">
            <span class="section-label">{{ currentLang === 'en' ? 'AUTHORIZED PARTNERS' : '授权合作伙伴' }}</span>
            <h2 class="section-title">
              {{ currentLang === 'en' ? 'Strong Partnerships,' : '强大的合作关系,' }}
              <span class="gradient-text">{{ currentLang === 'en' ? 'Greater Opportunities' : '更大的机遇' }}</span>
            </h2>
          </div>

          <div class="partners-showcase">
            <div v-for="partner in partners" :key="partner.index" class="partner-card">
              <div class="partner-badge">{{ partner.index }}</div>
              <div class="partner-logo">
                <span :class="{ 'text-cyan': partner.isCyan }">{{ partner.name }}</span>
              </div>
              <div class="partner-divider"></div>
              <span class="partner-role">{{ currentLang === 'en' ? partner.roleEn : partner.roleCn }}</span>
              <p class="partner-desc">{{ currentLang === 'en' ? partner.descEn : partner.descCn }}</p>
            </div>
          </div>
        </div>
      </section>

      <!-- ================= CAPABILITIES ================= -->
      <section class="capabilities" id="is-gelistirme">
        <div class="container">
          <div class="capabilities-wrapper">
            <div class="capabilities-content">
              <span class="section-label">{{ currentLang === 'en' ? 'WHY CHOOSE US' : '为什么选择我们' }}</span>
              <h2 class="section-title">
                {{ currentLang === 'en' ? 'Bringing Technology' : '将科技' }}
                <span class="gradient-text">{{ currentLang === 'en' ? 'to Market' : '推向市场' }}</span>
              </h2>
              <p class="capabilities-desc">
                {{ currentLang === 'en'
                  ? 'We create sales representation, channel development, customer access, and long-term business partnerships for global manufacturers to grow in the Turkey market.'
                  : '我们为全球制造商在土耳其市场的增长提供销售代理、渠道开发、客户对接和长期商业合作服务。'
                }}
              </p>
              <ul class="capability-list">
                <li v-for="cap in capabilities" :key="cap.labelEn">
                  <div class="cap-icon">
                    <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                      <polyline points="20 6 9 17 4 12"/>
                    </svg>
                  </div>
                  <span>{{ currentLang === 'en' ? cap.labelEn : cap.labelCn }}</span>
                </li>
              </ul>
            </div>
            <div class="capabilities-visual">
              <div class="visual-ring visual-ring-1"></div>
              <div class="visual-ring visual-ring-2"></div>
              <div class="visual-ring visual-ring-3"></div>
              <div class="visual-center">
                <svg width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
                  <polygon points="12 2 2 7 12 12 22 7 12 2"/>
                  <polyline points="2 17 12 22 22 17"/>
                  <polyline points="2 12 12 17 22 12"/>
                </svg>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- ================= ABOUT ================= -->
      <section class="about" id="hakkimizda">
        <div class="about-bg"></div>
        <div class="container">
          <div class="about-content">
            <span class="section-label section-label-light">ABOUT ASTRA TECHNIC</span>
            <h2 class="about-title">
              {{ currentLang === 'en' ? 'Ideas,' : '创意,' }}
              <span class="gradient-text">{{ currentLang === 'en' ? 'Meet Technologies' : '与科技相遇' }}</span>
            </h2>
            <p class="about-desc">
              {{ currentLang === 'en'
                ? 'Astra Technic establishes reliable commercial and technical connections between global manufacturers, supply sources, distribution channels, and technology companies in Turkey.'
                : 'Astra Technic 在全球制造商、供应商、分销渠道和土耳其科技公司之间建立可靠的商业和技术桥梁。'
              }}
            </p>
            <div class="about-cta">
              <a href="#iletisim" class="btn btn-primary btn-lg">
                {{ currentLang === 'en' ? 'Get in Touch' : '联系我们' }}
              </a>
            </div>
          </div>
        </div>
      </section>

      <!-- ================= RFQ ================= -->
      <section class="rfq" id="iletisim">
        <div class="container">
          <div class="rfq-wrapper">
            <div class="rfq-info">
              <span class="section-label">{{ currentLang === 'en' ? 'GET STARTED' : '开始合作' }}</span>
              <h2 class="section-title">
                {{ currentLang === 'en' ? "Let's Find the" : '让我们一起找到' }}
                <span class="gradient-text">{{ currentLang === 'en' ? 'Right Source' : '合适的供应商' }}</span>
              </h2>
              <p class="rfq-desc">
                {{ currentLang === 'en'
                  ? 'Send us part number, manufacturer, and quantity needed; we will contact you within 24 hours.'
                  : '请发送您的零件型号、制造商和需求数量，我们将在24小时内与您联系。'
                }}
              </p>
              <div class="contact-list">
                <div class="contact-item">
                  <div class="contact-icon">
                    <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
                      <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/>
                      <polyline points="22,6 12,13 2,6"/>
                    </svg>
                  </div>
                  <div>
                    <span class="contact-label">{{ currentLang === 'en' ? 'Email' : '邮箱' }}</span>
                    <a href="mailto:info@astratechnic.com">info@astratechnic.com</a>
                  </div>
                </div>
                <div class="contact-item">
                  <div class="contact-icon contact-icon-whatsapp">
                    <svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
                      <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347z"/>
                    </svg>
                  </div>
                  <div>
                    <span class="contact-label">WhatsApp</span>
                    <a href="#" @click.prevent="openWhatsApp">{{ currentLang === 'en' ? 'Chat directly' : '直接聊天' }}</a>
                  </div>
                </div>
              </div>
            </div>

            <form class="rfq-form" @submit.prevent="handleSubmit">
              <h3>{{ currentLang === 'en' ? 'Request for Quotation' : '询价请求' }}</h3>
              <div class="form-grid">
                <div class="form-group">
                  <label for="mpn">{{ currentLang === 'en' ? 'Part Number / MPN' : '零件型号 / MPN' }} *</label>
                  <input id="mpn" v-model="formData.mpn" type="text" required />
                </div>
                <div class="form-group">
                  <label for="manufacturer">{{ currentLang === 'en' ? 'Manufacturer' : '制造商' }}</label>
                  <input id="manufacturer" v-model="formData.manufacturer" type="text" />
                </div>
                <div class="form-group">
                  <label for="quantity">{{ currentLang === 'en' ? 'Quantity' : '数量' }}</label>
                  <input id="quantity" v-model="formData.quantity" type="number" min="1" />
                </div>
                <div class="form-group">
                  <label for="email">Email *</label>
                  <input id="email" v-model="formData.email" type="email" required />
                </div>
              </div>
              <div class="form-group form-group-full">
                <label for="notes">{{ currentLang === 'en' ? 'Notes' : '备注' }}</label>
                <textarea id="notes" v-model="formData.notes" rows="4"></textarea>
              </div>
              <button type="submit" class="btn btn-primary btn-lg btn-block">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <line x1="22" y1="2" x2="11" y2="13"/>
                  <polygon points="22 2 15 22 11 13 2 9 22 2"/>
                </svg>
                {{ currentLang === 'en' ? 'SEND RFQ' : '提交询价' }}
              </button>
              <p v-if="formStatus" class="form-status">{{ formStatus }}</p>
            </form>
          </div>
        </div>
      </section>
    </main>

    <!-- ================= FOOTER ================= -->
    <footer class="site-footer">
      <div class="container">
        <div class="footer-grid">
          <div class="footer-brand">
            <a href="#top" class="brand">
              <span class="brand-mark">
                <svg width="28" height="28" viewBox="0 0 32 32" fill="none">
                  <path d="M16 2L30 24H2L16 2Z" stroke="currentColor" stroke-width="2" stroke-linejoin="round"/>
                  <path d="M16 12L22 22H10L16 12Z" fill="currentColor"/>
                </svg>
              </span>
              <span class="brand-word">ASTRA<em>TECHNIC</em></span>
            </a>
            <p class="footer-tagline">GLOBAL CONNECTIONS. REAL OPPORTUNITIES.</p>
          </div>

          <div class="footer-nav">
            <h4>{{ currentLang === 'en' ? 'Quick Links' : '快速链接' }}</h4>
            <ul>
              <li><a href="#global-sourcing">{{ currentLang === 'en' ? 'Global Sourcing' : '全球采购' }}</a></li>
              <li><a href="#ortaklar">{{ currentLang === 'en' ? 'Our Partners' : '合作伙伴' }}</a></li>
              <li><a href="#is-gelistirme">{{ currentLang === 'en' ? 'Business Development' : '业务发展' }}</a></li>
              <li><a href="#danismanlik">{{ currentLang === 'en' ? 'Consulting' : '咨询服务' }}</a></li>
            </ul>
          </div>

          <div class="footer-contact">
            <h4>{{ currentLang === 'en' ? 'Contact' : '联系我们' }}</h4>
            <ul>
              <li>
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
                  <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/>
                  <polyline points="22,6 12,13 2,6"/>
                </svg>
                <a href="mailto:info@astratechnic.com">info@astratechnic.com</a>
              </li>
              <li>
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
                  <path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"/>
                  <circle cx="12" cy="10" r="3"/>
                </svg>
                <span>{{ currentLang === 'en' ? 'Istanbul, Turkey' : '土耳其，伊斯坦布尔' }}</span>
              </li>
            </ul>
          </div>

          <div class="footer-social">
            <h4>{{ currentLang === 'en' ? 'Follow Us' : '关注我们' }}</h4>
            <div class="social-links">
              <a href="#" @click.prevent="openWhatsApp" aria-label="WhatsApp">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
                  <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347z"/>
                </svg>
              </a>
              <a href="https://www.linkedin.com/" target="_blank" rel="noopener" aria-label="LinkedIn">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
                  <path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"/>
                  <rect x="2" y="9" width="4" height="12"/>
                  <circle cx="4" cy="4" r="2"/>
                </svg>
              </a>
            </div>
          </div>
        </div>

        <div class="footer-bottom">
          <p>&copy; 2026 Astra Technic. {{ currentLang === 'en' ? 'All rights reserved.' : '版权所有。' }}</p>
        </div>
      </div>
    </footer>

    <!-- floating WhatsApp -->
    <a href="#" class="whatsapp-float" @click.prevent="openWhatsApp" aria-label="WhatsApp">
      <svg width="28" height="28" viewBox="0 0 24 24" fill="currentColor">
        <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347z"/>
      </svg>
    </a>
  </div>
</template>

<style lang="scss" scoped>
// =============================================
// VARIABLES
// =============================================
$primary: #0f1923;
$primary-light: #1a2a3a;
$accent: #00c2cb;
$accent-dark: #00a8ae;
$cyan: #00d4d4;
$text: #ffffff;
$text-soft: rgba(255, 255, 255, 0.7);
$text-muted: rgba(255, 255, 255, 0.5);
$bg-dark: #0a131a;
$bg-card: rgba(255, 255, 255, 0.03);
$border: rgba(255, 255, 255, 0.08);

$font-heading: 'Space Grotesk', 'Noto Sans SC', system-ui, sans-serif;
$font-body: 'Inter', 'Noto Sans SC', system-ui, sans-serif;

// =============================================
// BASE
// =============================================
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.page-wrapper {
  min-height: 100vh;
  background: $primary;
  color: $text;
  font-family: $font-body;
  line-height: 1.6;
  overflow-x: hidden;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 24px;
}

// =============================================
// TYPOGRAPHY
// =============================================
.gradient-text {
  background: linear-gradient(135deg, $accent 0%, $cyan 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.section-label {
  display: inline-block;
  font-family: $font-heading;
  font-size: 12px;
  font-weight: 600;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: $accent;
  margin-bottom: 16px;
  padding: 8px 16px;
  background: rgba($accent, 0.1);
  border-radius: 20px;
  border: 1px solid rgba($accent, 0.2);
  
  &.section-label-light {
    background: rgba(255, 255, 255, 0.1);
    border-color: rgba(255, 255, 255, 0.2);
    color: $text-soft;
  }
}

.section-header {
  text-align: center;
  margin-bottom: 64px;
}

.section-title {
  font-family: $font-heading;
  font-size: clamp(32px, 5vw, 48px);
  font-weight: 700;
  line-height: 1.2;
  color: $text;
}

// =============================================
// BUTTONS
// =============================================
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  padding: 12px 24px;
  font-family: $font-heading;
  font-size: 14px;
  font-weight: 600;
  text-decoration: none;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.3s ease;
  border: none;

  svg {
    flex-shrink: 0;
  }

  &.btn-primary {
    background: linear-gradient(135deg, $accent 0%, $accent-dark 100%);
    color: $primary;
    box-shadow: 0 4px 20px rgba($accent, 0.3);

    &:hover {
      transform: translateY(-2px);
      box-shadow: 0 8px 30px rgba($accent, 0.4);
    }
  }

  &.btn-outline {
    background: transparent;
    color: $text;
    border: 1px solid rgba($text, 0.3);

    &:hover {
      border-color: $text;
      background: rgba($text, 0.05);
    }
  }

  &.btn-lg {
    padding: 16px 32px;
    font-size: 15px;
  }

  &.btn-block {
    width: 100%;
  }
}

// =============================================
// HEADER
// =============================================
.site-header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 100;
  background: rgba($primary, 0.95);
  backdrop-filter: blur(20px);
  border-bottom: 1px solid $border;
}

.header-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 80px;
}

.brand {
  display: flex;
  align-items: center;
  gap: 12px;
  text-decoration: none;
  color: $text;
}

.brand-mark {
  color: $accent;
}

.brand-word {
  font-family: $font-heading;
  font-size: 20px;
  font-weight: 700;
  letter-spacing: 0.02em;

  em {
    font-style: normal;
    color: $accent;
  }
}

.primary-nav ul {
  display: flex;
  list-style: none;
  gap: 40px;

  a {
    color: $text-soft;
    text-decoration: none;
    font-size: 14px;
    font-weight: 500;
    transition: color 0.2s;
    position: relative;

    &::after {
      content: '';
      position: absolute;
      bottom: -4px;
      left: 0;
      width: 0;
      height: 2px;
      background: $accent;
      transition: width 0.3s ease;
    }

    &:hover {
      color: $text;
      
      &::after {
        width: 100%;
      }
    }
  }
}

.header-actions {
  display: flex;
  align-items: center;
  gap: 20px;
}

.lang-switch {
  background: none;
  border: 1px solid $border;
  color: $text-soft;
  font-size: 13px;
  font-weight: 500;
  cursor: pointer;
  padding: 8px 12px;
  border-radius: 6px;
  transition: all 0.2s;

  span {
    transition: color 0.2s;
    
    &.is-active {
      color: $accent;
    }
  }

  .lang-sep {
    margin: 0 6px;
    opacity: 0.4;
  }

  &:hover {
    border-color: $accent;
  }
}

.nav-toggle {
  display: none;
  flex-direction: column;
  gap: 5px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 8px;

  span {
    width: 24px;
    height: 2px;
    background: $text;
    border-radius: 1px;
  }
}

// =============================================
// HERO
// =============================================
.hero {
  position: relative;
  min-height: 100vh;
  display: flex;
  align-items: center;
  padding-top: 80px;
  overflow: hidden;
}

.hero-bg {
  position: absolute;
  inset: 0;
  z-index: 0;
}

.hero-gradient {
  position: absolute;
  inset: 0;
  background: 
    radial-gradient(ellipse 80% 50% at 50% 0%, rgba($accent, 0.15) 0%, transparent 50%),
    radial-gradient(ellipse 60% 40% at 80% 50%, rgba($cyan, 0.1) 0%, transparent 50%),
    linear-gradient(180deg, $primary 0%, $primary-light 50%, $primary 100%);
}

.hero-grid {
  position: absolute;
  inset: 0;
  background-image: 
    linear-gradient(rgba($accent, 0.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba($accent, 0.03) 1px, transparent 1px);
  background-size: 60px 60px;
  mask-image: radial-gradient(ellipse at center, black 30%, transparent 70%);
}

.hero-glow {
  position: absolute;
  border-radius: 50%;
  filter: blur(100px);
  animation: float 8s ease-in-out infinite;
  
  &.hero-glow-1 {
    width: 600px;
    height: 600px;
    background: rgba($accent, 0.15);
    top: -200px;
    right: -200px;
  }
  
  &.hero-glow-2 {
    width: 400px;
    height: 400px;
    background: rgba($cyan, 0.1);
    bottom: -100px;
    left: -100px;
    animation-delay: -4s;
  }
}

@keyframes float {
  0%, 100% { transform: translate(0, 0); }
  50% { transform: translate(-30px, 30px); }
}

.hero-content {
  position: relative;
  z-index: 1;
  display: grid;
  grid-template-columns: 1.2fr 1fr;
  gap: 80px;
  align-items: center;
  padding: 80px 0;
}

.hero-badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 8px 16px;
  background: rgba($accent, 0.1);
  border: 1px solid rgba($accent, 0.2);
  border-radius: 30px;
  font-size: 13px;
  color: $text-soft;
  margin-bottom: 24px;

  .badge-dot {
    width: 8px;
    height: 8px;
    background: $accent;
    border-radius: 50%;
    animation: pulse-dot 2s ease-in-out infinite;
  }
}

@keyframes pulse-dot {
  0%, 100% { opacity: 1; transform: scale(1); }
  50% { opacity: 0.5; transform: scale(1.2); }
}

.hero-title {
  font-family: $font-heading;
  font-size: clamp(40px, 6vw, 64px);
  font-weight: 700;
  line-height: 1.1;
  margin-bottom: 24px;
  color: $text;
}

.hero-description {
  font-size: 18px;
  color: $text-soft;
  line-height: 1.7;
  margin-bottom: 40px;
  max-width: 520px;
}

.hero-stats {
  display: flex;
  align-items: center;
  gap: 32px;
  margin-bottom: 40px;
  padding: 24px 0;
  border-top: 1px solid $border;
  border-bottom: 1px solid $border;
}

.stat-item {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.stat-number {
  font-family: $font-heading;
  font-size: 32px;
  font-weight: 700;
  color: $accent;
}

.stat-label {
  font-size: 13px;
  color: $text-muted;
}

.stat-divider {
  width: 1px;
  height: 48px;
  background: $border;
}

.hero-actions {
  display: flex;
  gap: 16px;
  flex-wrap: wrap;
}

.hero-visual {
  position: relative;
  height: 400px;
}

.visual-card {
  position: absolute;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 12px;
  padding: 24px;
  background: rgba($primary-light, 0.8);
  backdrop-filter: blur(10px);
  border: 1px solid $border;
  border-radius: 16px;
  animation: float-card 6s ease-in-out infinite;

  .card-icon {
    width: 64px;
    height: 64px;
    display: flex;
    align-items: center;
    justify-content: center;
    background: linear-gradient(135deg, rgba($accent, 0.2) 0%, rgba($cyan, 0.1) 100%);
    border-radius: 12px;
    color: $accent;
  }

  span {
    font-size: 13px;
    font-weight: 500;
    color: $text-soft;
  }

  &.visual-card-1 {
    top: 20%;
    left: 10%;
    animation-delay: 0s;
  }

  &.visual-card-2 {
    top: 45%;
    right: 5%;
    animation-delay: -2s;
  }

  &.visual-card-3 {
    bottom: 15%;
    left: 25%;
    animation-delay: -4s;
  }
}

@keyframes float-card {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-15px); }
}

.scroll-indicator {
  position: absolute;
  bottom: 40px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 12px;
  color: $text-muted;
  font-size: 12px;
  text-transform: uppercase;
  letter-spacing: 0.1em;
}

.scroll-mouse {
  width: 24px;
  height: 36px;
  border: 2px solid $text-muted;
  border-radius: 12px;
  position: relative;
}

.scroll-wheel {
  width: 4px;
  height: 8px;
  background: $accent;
  border-radius: 2px;
  position: absolute;
  top: 6px;
  left: 50%;
  transform: translateX(-50%);
  animation: scroll-wheel 2s ease-in-out infinite;
}

@keyframes scroll-wheel {
  0% { opacity: 1; top: 6px; }
  100% { opacity: 0; top: 20px; }
}

// =============================================
// SERVICES
// =============================================
.services {
  padding: 120px 0;
  background: linear-gradient(180deg, $primary 0%, $bg-dark 100%);
}

.services-grid {
  display: grid;
  grid-template-columns: 1.5fr 1fr 1fr;
  gap: 24px;
}

.service-card {
  padding: 40px;
  background: $bg-card;
  border: 1px solid $border;
  border-radius: 20px;
  transition: all 0.3s ease;

  &:hover {
    border-color: rgba($accent, 0.3);
    transform: translateY(-4px);
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
  }

  &.service-card-main {
    background: linear-gradient(135deg, rgba($accent, 0.1) 0%, rgba($cyan, 0.05) 100%);
    border-color: rgba($accent, 0.2);
  }

  .service-icon {
    width: 72px;
    height: 72px;
    display: flex;
    align-items: center;
    justify-content: center;
    background: linear-gradient(135deg, rgba($accent, 0.2) 0%, rgba($cyan, 0.1) 100%);
    border-radius: 16px;
    color: $accent;
    margin-bottom: 24px;
  }

  h3 {
    font-family: $font-heading;
    font-size: 22px;
    font-weight: 600;
    margin-bottom: 12px;
    color: $text;
  }

  p {
    font-size: 15px;
    color: $text-soft;
    line-height: 1.7;
    margin-bottom: 24px;
  }
}

.feature-list {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 12px;
  margin-bottom: 24px;

  li {
    display: flex;
    align-items: center;
    gap: 12px;
    font-size: 14px;
    color: $text-soft;

    svg {
      color: $accent;
      flex-shrink: 0;
    }
  }
}

.service-link {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  font-size: 14px;
  font-weight: 600;
  color: $accent;
  text-decoration: none;
  transition: gap 0.2s;

  &:hover {
    gap: 12px;
  }
}

// =============================================
// PARTNERS
// =============================================
.partners {
  position: relative;
  padding: 120px 0;
  overflow: hidden;
}

.partners-bg {
  position: absolute;
  inset: 0;
  background: linear-gradient(180deg, $bg-dark 0%, $primary 100%);
}

.partners-pattern {
  position: absolute;
  inset: 0;
  opacity: 0.5;
  background-image: radial-gradient(rgba($accent, 0.1) 1px, transparent 1px);
  background-size: 30px 30px;
}

.partners-showcase {
  position: relative;
  z-index: 1;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 32px;
  max-width: 900px;
  margin: 0 auto;
}

.partner-card {
  position: relative;
  padding: 48px;
  background: rgba($primary-light, 0.6);
  backdrop-filter: blur(10px);
  border: 1px solid $border;
  border-radius: 20px;
  text-align: center;
  transition: all 0.3s ease;

  &:hover {
    transform: translateY(-4px);
    border-color: rgba($accent, 0.3);
    box-shadow: 0 20px 50px rgba(0, 0, 0, 0.3);

    .partner-badge {
      transform: translateX(-50%) scale(1.1);
    }
  }
}

.partner-badge {
  position: absolute;
  top: -16px;
  left: 50%;
  transform: translateX(-50%);
  padding: 8px 20px;
  background: linear-gradient(135deg, $accent 0%, $accent-dark 100%);
  border-radius: 20px;
  font-family: $font-heading;
  font-size: 12px;
  font-weight: 700;
  color: $primary;
  transition: transform 0.3s ease;
}

.partner-logo {
  margin-bottom: 24px;
  
  span {
    font-family: $font-heading;
    font-size: 28px;
    font-weight: 700;
    letter-spacing: 0.1em;
    color: $text;
    
    &.text-cyan {
      color: $cyan;
    }
  }
}

.partner-divider {
  width: 60px;
  height: 2px;
  background: linear-gradient(90deg, transparent, $accent, transparent);
  margin: 0 auto 16px;
}

.partner-role {
  display: block;
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: $text-muted;
  margin-bottom: 16px;
}

.partner-desc {
  font-size: 15px;
  color: $text-soft;
  line-height: 1.6;
}

// =============================================
// CAPABILITIES
// =============================================
.capabilities {
  padding: 120px 0;
  background: $primary;
}

.capabilities-wrapper {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 80px;
  align-items: center;
}

.capabilities-content {
  .section-label {
    margin-bottom: 16px;
  }

  .section-title {
    margin-bottom: 24px;
  }
}

.capabilities-desc {
  font-size: 16px;
  color: $text-soft;
  line-height: 1.7;
  margin-bottom: 40px;
}

.capability-list {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 20px;

  li {
    display: flex;
    align-items: center;
    gap: 16px;
    font-size: 16px;
    color: $text;
  }
}

.cap-icon {
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba($accent, 0.1);
  border: 1px solid rgba($accent, 0.2);
  border-radius: 10px;
  color: $accent;
  flex-shrink: 0;
}

.capabilities-visual {
  position: relative;
  height: 400px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.visual-ring {
  position: absolute;
  border: 1px solid rgba($accent, 0.2);
  border-radius: 50%;
  animation: ring-pulse 4s ease-in-out infinite;

  &.visual-ring-1 {
    width: 300px;
    height: 300px;
  }

  &.visual-ring-2 {
    width: 220px;
    height: 220px;
    animation-delay: -1s;
  }

  &.visual-ring-3 {
    width: 140px;
    height: 140px;
    animation-delay: -2s;
  }
}

@keyframes ring-pulse {
  0%, 100% { transform: scale(1); opacity: 1; }
  50% { transform: scale(1.05); opacity: 0.7; }
}

.visual-center {
  width: 100px;
  height: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, rgba($accent, 0.2) 0%, rgba($cyan, 0.1) 100%);
  border: 1px solid rgba($accent, 0.3);
  border-radius: 24px;
  color: $accent;
  z-index: 1;
}

// =============================================
// ABOUT
// =============================================
.about {
  position: relative;
  padding: 160px 0;
  overflow: hidden;
}

.about-bg {
  position: absolute;
  inset: 0;
  background: 
    radial-gradient(ellipse 80% 50% at 50% 50%, rgba($accent, 0.1) 0%, transparent 50%),
    linear-gradient(180deg, $bg-dark 0%, $primary 100%);
}

.about-content {
  position: relative;
  z-index: 1;
  text-align: center;
  max-width: 800px;
  margin: 0 auto;
}

.about-title {
  font-family: $font-heading;
  font-size: clamp(40px, 6vw, 56px);
  font-weight: 700;
  line-height: 1.15;
  margin-bottom: 24px;
}

.about-desc {
  font-size: 18px;
  color: $text-soft;
  line-height: 1.8;
  margin-bottom: 40px;
}

// =============================================
// RFQ
// =============================================
.rfq {
  padding: 120px 0;
  background: linear-gradient(180deg, $primary 0%, $bg-dark 100%);
}

.rfq-wrapper {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 80px;
  align-items: start;
}

.rfq-info {
  .section-label {
    margin-bottom: 16px;
  }

  .section-title {
    margin-bottom: 24px;
  }
}

.rfq-desc {
  font-size: 16px;
  color: $text-soft;
  line-height: 1.7;
  margin-bottom: 40px;
}

.contact-list {
  display: flex;
  flex-direction: column;
  gap: 24px;
}

.contact-item {
  display: flex;
  align-items: center;
  gap: 16px;

  > div {
    display: flex;
    flex-direction: column;
    gap: 4px;
  }

  a {
    color: $text;
    text-decoration: none;
    font-weight: 500;
    transition: color 0.2s;

    &:hover {
      color: $accent;
    }
  }
}

.contact-icon {
  width: 48px;
  height: 48px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba($accent, 0.1);
  border: 1px solid rgba($accent, 0.2);
  border-radius: 12px;
  color: $accent;

  &.contact-icon-whatsapp {
    background: rgba(#25D366, 0.1);
    border-color: rgba(#25D366, 0.2);
    color: #25D366;
  }
}

.contact-label {
  font-size: 12px;
  color: $text-muted;
  text-transform: uppercase;
  letter-spacing: 0.1em;
}

.rfq-form {
  padding: 48px;
  background: rgba($primary-light, 0.5);
  backdrop-filter: blur(10px);
  border: 1px solid $border;
  border-radius: 24px;

  h3 {
    font-family: $font-heading;
    font-size: 24px;
    font-weight: 600;
    margin-bottom: 32px;
    color: $text;
  }
}

.form-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
  margin-bottom: 20px;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 8px;

  &.form-group-full {
    grid-column: 1 / -1;
    margin-bottom: 24px;
  }

  label {
    font-size: 13px;
    font-weight: 500;
    color: $text-soft;
  }

  input,
  textarea {
    padding: 14px 18px;
    background: rgba($text, 0.03);
    border: 1px solid $border;
    border-radius: 10px;
    color: $text;
    font-size: 15px;
    font-family: inherit;
    transition: all 0.2s;

    &:focus {
      outline: none;
      border-color: $accent;
      background: rgba($accent, 0.05);
    }

    &::placeholder {
      color: $text-muted;
    }
  }

  textarea {
    resize: vertical;
    min-height: 100px;
  }
}

.form-status {
  margin-top: 16px;
  font-size: 14px;
  color: $accent;
  text-align: center;
}

// =============================================
// FOOTER
// =============================================
.site-footer {
  padding: 80px 0 40px;
  background: $bg-dark;
  border-top: 1px solid $border;
}

.footer-grid {
  display: grid;
  grid-template-columns: 1.5fr 1fr 1fr 1fr;
  gap: 48px;
  margin-bottom: 48px;
}

.footer-brand {
  .brand {
    margin-bottom: 16px;
  }

  .footer-tagline {
    font-size: 12px;
    font-weight: 500;
    letter-spacing: 0.1em;
    color: $text-muted;
  }
}

.footer-nav,
.footer-contact,
.footer-social {
  h4 {
    font-family: $font-heading;
    font-size: 14px;
    font-weight: 600;
    color: $text;
    margin-bottom: 20px;
    text-transform: uppercase;
    letter-spacing: 0.05em;
  }

  ul {
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: 12px;
  }

  a {
    color: $text-soft;
    text-decoration: none;
    font-size: 14px;
    transition: color 0.2s;

    &:hover {
      color: $accent;
    }
  }

  li {
    display: flex;
    align-items: center;
    gap: 10px;
    color: $text-soft;
    font-size: 14px;
  }
}

.social-links {
  display: flex;
  gap: 12px;

  a {
    width: 44px;
    height: 44px;
    display: flex;
    align-items: center;
    justify-content: center;
    background: rgba($text, 0.05);
    border: 1px solid $border;
    border-radius: 10px;
    color: $text-soft;
    transition: all 0.2s;

    &:hover {
      background: $accent;
      border-color: $accent;
      color: $primary;
    }
  }
}

.footer-bottom {
  padding-top: 32px;
  border-top: 1px solid $border;
  text-align: center;

  p {
    font-size: 13px;
    color: $text-muted;
  }
}

// =============================================
// WHATSAPP FLOAT
// =============================================
.whatsapp-float {
  position: fixed;
  bottom: 32px;
  right: 32px;
  z-index: 99;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 60px;
  height: 60px;
  background: #25D366;
  border-radius: 50%;
  box-shadow: 0 4px 20px rgba(#25D366, 0.4);
  transition: all 0.3s ease;
  color: white;
  text-decoration: none;

  &:hover {
    transform: scale(1.1);
    box-shadow: 0 8px 30px rgba(#25D366, 0.5);
  }
}

// =============================================
// RESPONSIVE
// =============================================
@media (max-width: 1024px) {
  .hero-content {
    grid-template-columns: 1fr;
    text-align: center;
  }

  .hero-visual {
    display: none;
  }

  .hero-description {
    margin-left: auto;
    margin-right: auto;
  }

  .hero-stats {
    justify-content: center;
  }

  .hero-actions {
    justify-content: center;
  }

  .services-grid {
    grid-template-columns: 1fr;
  }

  .capabilities-wrapper {
    grid-template-columns: 1fr;
  }

  .capabilities-visual {
    display: none;
  }

  .rfq-wrapper {
    grid-template-columns: 1fr;
  }

  .footer-grid {
    grid-template-columns: 1fr 1fr;
  }
}

@media (max-width: 768px) {
  .primary-nav {
    display: none;
  }

  .nav-toggle {
    display: flex;
  }

  .section-title {
    font-size: 28px;
  }

  .hero-stats {
    flex-wrap: wrap;
    gap: 24px;
  }

  .stat-divider {
    display: none;
  }

  .partners-showcase {
    grid-template-columns: 1fr;
  }

  .form-grid {
    grid-template-columns: 1fr;
  }

  .footer-grid {
    grid-template-columns: 1fr;
    text-align: center;
  }

  .footer-nav ul,
  .footer-contact ul {
    align-items: center;
  }

  .social-links {
    justify-content: center;
  }

  .scroll-indicator {
    display: none;
  }
}
</style>
