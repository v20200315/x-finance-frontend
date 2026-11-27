<script setup lang="ts">
import type { Component } from 'vue'
import { nextTick, ref } from 'vue'
import { useRouter } from 'vue-router'
import {
  Close,
  DataAnalysis,
  Document,
  Menu as MenuIcon,
  TrendCharts,
} from '@element-plus/icons-vue'

interface Metric {
  label: string
  value: string
  note: string
}

interface Feature {
  title: string
  description: string
  icon: Component
}

const router = useRouter()
const menuOpen = ref(false)

const metrics: Metric[] = [
  { label: 'Total Assets', value: '¥12,486,200', note: 'Period balance' },
  { label: 'Total Liabilities', value: '¥4,273,800', note: 'Period balance' },
  { label: 'Current Revenue', value: '¥2,845,600', note: 'Year to date' },
  { label: 'Net Profit', value: '¥618,400', note: 'Year to date' },
]

const features: Feature[] = [
  {
    title: 'Accounting Management',
    description:
      'Manage accounting vouchers, accounting subjects, and financial records in one place.',
    icon: Document,
  },
  {
    title: 'Financial Reporting',
    description:
      'Generate balance sheets, income statements, and accounting reports with clarity.',
    icon: DataAnalysis,
  },
  {
    title: 'Financial Insights',
    description:
      'Understand financial performance through structured data and meaningful indicators.',
    icon: TrendCharts,
  },
]

function goDashboard() {
  menuOpen.value = false
  void router.push('/dashboard')
}

async function scrollTo(id: string) {
  menuOpen.value = false
  await nextTick()
  await new Promise<void>((resolve) => {
    requestAnimationFrame(() => resolve())
  })

  const target = document.getElementById(id)
  const header = document.querySelector('.header')
  if (!target || !(header instanceof HTMLElement)) return

  const top =
    target.getBoundingClientRect().top +
    window.scrollY -
    header.getBoundingClientRect().height -
    16
  window.scrollTo({ top, behavior: 'smooth' })
}
</script>

<template>
  <div class="landing">
    <header class="header">
      <div class="container header-bar">
        <a class="brand" href="#top" @click.prevent="scrollTo('top')">
          <span class="brand-mark" aria-hidden="true">X</span>
          <span>X Finance</span>
        </a>

        <nav class="nav" aria-label="Primary">
          <a href="#features" @click.prevent="scrollTo('features')">Features</a>
          <a href="#about" @click.prevent="scrollTo('about')">About</a>
        </nav>

        <div class="header-actions">
          <button
            class="nav-toggle"
            type="button"
            :aria-expanded="menuOpen"
            aria-controls="mobile-nav"
            @click="menuOpen = !menuOpen"
          >
            <el-icon :size="18">
              <Close v-if="menuOpen" />
              <MenuIcon v-else />
            </el-icon>
            <span class="sr-only">{{
              menuOpen ? 'Close menu' : 'Open menu'
            }}</span>
          </button>
          <el-button type="primary" @click="goDashboard">Sign In</el-button>
        </div>
      </div>

      <nav
        id="mobile-nav"
        class="mobile-nav"
        :class="{ 'is-open': menuOpen }"
        aria-label="Mobile"
      >
        <a href="#features" @click.prevent="scrollTo('features')">Features</a>
        <a href="#about" @click.prevent="scrollTo('about')">About</a>
      </nav>
    </header>

    <main id="top">
      <section class="hero">
        <div class="container hero-copy">
          <p class="eyebrow">Accounting for growing businesses</p>
          <h1>Financial Clarity. Better Decisions.</h1>
          <p class="lede">
            A modern financial management platform designed to simplify
            accounting, improve financial visibility, and support better
            business decisions.
          </p>
          <div class="hero-actions">
            <el-button type="primary" size="large" @click="goDashboard">
              Get Started
            </el-button>
            <el-button size="large" @click="scrollTo('features')">
              Explore Features
            </el-button>
          </div>
        </div>
      </section>

      <section class="preview-section" aria-label="Product preview">
        <div class="container">
          <article class="preview">
            <header class="preview-head">
              <div>
                <h2>Financial overview</h2>
                <p>March 2026 · sample figures</p>
              </div>
              <span class="sample-tag">Sample data</span>
            </header>

            <div class="metrics">
              <div v-for="metric in metrics" :key="metric.label" class="metric">
                <p class="metric-label">{{ metric.label }}</p>
                <p class="metric-value">{{ metric.value }}</p>
                <p class="metric-note">{{ metric.note }}</p>
              </div>
            </div>

            <div class="composition">
              <p class="composition-label">Balance sheet composition</p>
              <div class="composition-track" aria-hidden="true">
                <span class="composition-assets" />
                <span class="composition-liabilities" />
              </div>
              <div class="composition-legend">
                <span><i class="swatch assets" /> Assets 74.5%</span>
                <span><i class="swatch liabilities" /> Liabilities 25.5%</span>
              </div>
            </div>
          </article>
        </div>
      </section>

      <section id="features" class="section">
        <div class="container">
          <div class="section-heading">
            <h2>Features</h2>
            <p>The core of day-to-day accounting, reporting, and review.</p>
          </div>
          <div class="feature-grid">
            <article
              v-for="feature in features"
              :key="feature.title"
              class="feature-card"
            >
              <span class="feature-icon">
                <el-icon :size="22">
                  <component :is="feature.icon" />
                </el-icon>
              </span>
              <h3>{{ feature.title }}</h3>
              <p>{{ feature.description }}</p>
            </article>
          </div>
        </div>
      </section>

      <section id="about" class="section about">
        <div class="container about-panel">
          <h2>About</h2>
          <p>
            X Finance is designed to make enterprise accounting more accessible,
            structured, and transparent.
          </p>
        </div>
      </section>
    </main>

    <footer class="footer">
      <div class="container footer-inner">
        <div>
          <p class="footer-brand">X Finance</p>
          <p class="footer-copy">
            A lightweight accounting platform for small and medium-sized
            businesses.
          </p>
        </div>
        <p class="copyright">© 2026 X Finance. All rights reserved.</p>
      </div>
    </footer>
  </div>
</template>

<style scoped>
.landing {
  --navy: #10243f;
  --muted: #5c6b80;
  --line: #e6e8ee;
  --card: #ffffff;
  --page: #f6f7f9;
  --accent-soft: #eef2ff;
  min-height: 100vh;
  background: var(--page);
  color: var(--navy);
}

.container {
  width: min(1120px, calc(100% - 48px));
  margin: 0 auto;
}

.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}

.header {
  position: sticky;
  top: 0;
  z-index: 20;
  background: rgba(255, 255, 255, 0.92);
  border-bottom: 1px solid var(--line);
  backdrop-filter: blur(12px);
}

.header-bar {
  display: flex;
  align-items: center;
  gap: 24px;
  min-height: 68px;
}

.brand {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  color: var(--navy);
  font-size: 16px;
  font-weight: 600;
  letter-spacing: -0.02em;
  text-decoration: none;
  white-space: nowrap;
}

.brand-mark {
  display: grid;
  place-items: center;
  width: 28px;
  height: 28px;
  border-radius: 8px;
  background: var(--navy);
  color: #fff;
  font-size: 14px;
  font-weight: 700;
}

.nav {
  display: flex;
  align-items: center;
  gap: 28px;
  margin-left: 12px;
}

.nav a,
.mobile-nav a {
  color: var(--navy);
  font-size: 14px;
  font-weight: 500;
  text-decoration: none;
}

.nav a:hover,
.mobile-nav a:hover {
  color: var(--color-primary);
}

.header-actions {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-left: auto;
}

.nav-toggle {
  display: none;
  align-items: center;
  justify-content: center;
  width: 36px;
  height: 36px;
  padding: 0;
  border: 1px solid var(--line);
  border-radius: 8px;
  background: #fff;
  color: var(--navy);
  cursor: pointer;
}

.mobile-nav {
  display: none;
}

.hero {
  padding: 88px 0 28px;
}

.hero-copy {
  max-width: 760px;
}

.eyebrow {
  margin: 0 0 16px;
  color: var(--color-primary);
  font-size: 13px;
  font-weight: 600;
  letter-spacing: 0.04em;
  text-transform: uppercase;
}

.hero h1 {
  max-width: 14ch;
  color: var(--navy);
  font-size: 56px;
  font-weight: 600;
  letter-spacing: -0.035em;
  line-height: 1.08;
}

.lede {
  max-width: 62ch;
  margin: 20px 0 0;
  color: var(--muted);
  font-size: 18px;
  line-height: 1.65;
}

.hero-actions {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  margin-top: 32px;
}

.preview-section {
  padding: 28px 0 16px;
}

.preview {
  padding: 28px;
  border: 1px solid var(--line);
  border-radius: 16px;
  background: var(--card);
  box-shadow: 0 16px 40px rgba(16, 36, 63, 0.06);
}

.preview-head {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 16px;
  margin-bottom: 24px;
}

.preview-head h2,
.section-heading h2,
.about-panel h2 {
  color: var(--navy);
  font-size: 20px;
  font-weight: 600;
  letter-spacing: -0.02em;
}

.preview-head p,
.section-heading p,
.metric-note,
.composition-label,
.footer-copy {
  margin: 6px 0 0;
  color: var(--muted);
  font-size: 14px;
  line-height: 1.6;
}

.sample-tag {
  flex-shrink: 0;
  padding: 4px 10px;
  border-radius: 999px;
  background: var(--accent-soft);
  color: var(--color-primary);
  font-size: 12px;
  font-weight: 600;
}

.metrics {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 12px;
}

.metric {
  padding: 18px 16px;
  border: 1px solid var(--line);
  border-radius: 12px;
  background: #fbfcfd;
}

.metric-label {
  margin: 0;
  color: var(--muted);
  font-size: 13px;
}

.metric-value {
  margin: 10px 0 0;
  color: var(--navy);
  font-size: 22px;
  font-weight: 600;
  letter-spacing: -0.03em;
  line-height: 1.2;
}

.metric-note {
  margin-top: 8px;
  font-size: 12px;
}

.composition {
  margin-top: 22px;
}

.composition-track {
  display: flex;
  height: 10px;
  margin-top: 10px;
  overflow: hidden;
  border-radius: 999px;
  background: #e7ebf2;
}

.composition-assets {
  width: 74.5%;
  background: var(--navy);
}

.composition-liabilities {
  width: 25.5%;
  background: #8ea0b8;
}

.composition-legend {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
  margin-top: 10px;
  color: var(--muted);
  font-size: 13px;
}

.composition-legend span {
  display: inline-flex;
  align-items: center;
  gap: 8px;
}

.swatch {
  width: 8px;
  height: 8px;
  border-radius: 99px;
}

.swatch.assets {
  background: var(--navy);
}

.swatch.liabilities {
  background: #8ea0b8;
}

.section {
  padding: 72px 0;
  scroll-margin-top: 84px;
}

.section-heading {
  max-width: 560px;
  margin-bottom: 28px;
}

.section-heading h2,
.about-panel h2 {
  font-size: 32px;
  letter-spacing: -0.03em;
}

.feature-grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 16px;
}

.feature-card {
  padding: 24px;
  border: 1px solid var(--line);
  border-radius: 16px;
  background: var(--card);
  box-shadow: 0 8px 24px rgba(16, 36, 63, 0.04);
}

.feature-icon {
  display: grid;
  place-items: center;
  width: 42px;
  height: 42px;
  margin-bottom: 18px;
  border-radius: 12px;
  background: var(--accent-soft);
  color: var(--color-primary);
}

.feature-card h3 {
  color: var(--navy);
  font-size: 18px;
  font-weight: 600;
}

.feature-card p,
.about-panel p {
  margin: 10px 0 0;
  color: var(--muted);
  font-size: 15px;
  line-height: 1.65;
}

.about-panel {
  max-width: 760px;
  padding: 36px 40px;
  border: 1px solid var(--line);
  border-left: 3px solid var(--color-primary);
  border-radius: 16px;
  background: var(--card);
}

.footer {
  background: var(--navy);
  color: #d5dce6;
}

.footer-inner {
  display: flex;
  align-items: flex-end;
  justify-content: space-between;
  gap: 24px;
  padding: 40px 0;
}

.footer-brand {
  margin: 0;
  color: #fff;
  font-size: 16px;
  font-weight: 600;
}

.footer-copy {
  max-width: 42ch;
  color: #b7c2d0;
}

.copyright {
  margin: 0;
  color: #b7c2d0;
  font-size: 13px;
  white-space: nowrap;
}

@media (max-width: 900px) {
  .metrics,
  .feature-grid {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }

  .feature-grid {
    grid-template-columns: 1fr;
  }

  .hero h1 {
    font-size: 44px;
  }
}

@media (max-width: 720px) {
  .container {
    width: min(1120px, calc(100% - 32px));
  }

  .nav {
    display: none;
  }

  .nav-toggle {
    display: inline-flex;
  }

  .mobile-nav {
    display: none;
    flex-direction: column;
    gap: 4px;
    padding: 0 16px 12px;
  }

  .mobile-nav.is-open {
    display: flex;
  }

  .mobile-nav a {
    padding: 12px 8px;
    border-radius: 8px;
  }

  .mobile-nav a:hover {
    background: var(--accent-soft);
  }

  .hero {
    padding: 48px 0 12px;
  }

  .hero h1 {
    max-width: none;
    font-size: 34px;
  }

  .lede {
    font-size: 16px;
  }

  .preview {
    padding: 18px;
  }

  .metrics {
    grid-template-columns: 1fr;
  }

  .metric-value {
    font-size: 20px;
  }

  .section {
    padding: 48px 0;
  }

  .section-heading h2,
  .about-panel h2 {
    font-size: 26px;
  }

  .about-panel {
    padding: 24px;
  }

  .footer-inner {
    flex-direction: column;
    align-items: flex-start;
  }

  .copyright {
    white-space: normal;
  }
}
</style>
