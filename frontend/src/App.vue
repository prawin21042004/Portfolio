<template>
  <div id="app">
    <!-- ===================== NAVBAR ===================== -->
    <nav class="navbar">
      <div class="logo">
        <span class="logo-bracket">&lt;/&gt;</span>
        <span class="logo-text">Prawin <span class="accent">Kumar</span></span>
      </div>

      <ul class="nav-links" :class="{ 'nav-links-open': mobileMenuOpen }">
        <li><a href="#home" @click="closeMenu">Home</a></li>
        <li><a href="#about" @click="closeMenu">About</a></li>
        <li><a href="#skills" @click="closeMenu">Skills</a></li>
        <li><a href="#projects" @click="closeMenu">Projects</a></li>
        <li><a href="#contact" @click="closeMenu">Contact</a></li>
      </ul>

      <div class="navbar-actions">
        <button class="btn btn-outline download-btn">Download CV</button>

        <button
          class="hamburger"
          :class="{ active: mobileMenuOpen }"
          @click="toggleMenu"
          :aria-expanded="mobileMenuOpen"
          aria-label="Toggle navigation menu"
        >
          <span></span>
          <span></span>
          <span></span>
        </button>
      </div>
    </nav>

    <div class="nav-backdrop" v-if="mobileMenuOpen" @click="closeMenu"></div>

    <!-- ===================== HERO ===================== -->
    <section id="home" class="hero">
      <div class="hero-text">
        <h1 class="hero-title">
          Prawin <span class="accent">Kumar</span>
        </h1>
        <h2 class="hero-subtitle">Full Stack Developer</h2>
        <p class="hero-description">
          I build exceptional digital experience that are fast, accessible,
          visually appealing and responsive.<br />
          Let's build something amazing together!
        </p>

        <div class="hero-buttons">
          <button class="btn btn-primary">
            Hire me <span class="arrow">&#8594;</span>
          </button>
          <button class="btn btn-outline">View Projects</button>
        </div>
      </div>

      <div class="hero-image">
        <div class="image-circle"></div>
        <img
          :src="profileImage"
          alt="Prawin Kumar"
          class="profile-img"
        />
      </div>
    </section>

    <!-- ===================== ABOUT ===================== -->
    <section id="about" class="about-wrapper">
      <div class="about-image">
        <div class="image-card">
          <img
            :src="profileImage"
            alt="Prawin Kumar"
            class="about-profile-img"
          />
        </div>
      </div>

      <div class="about-text">
        <h2 class="about-title">About&nbsp; Me</h2>

        <p class="about-paragraph">
          I am a Python Full Stack Developer focused on building
          production-ready web applications. I enjoy designing robust APIs,
          developing interactive user interfaces, and optimizing applications
          to deliver smooth and efficient user experiences.
        </p>

        <p class="about-paragraph">
          Along with strong problem-solving skills, I follow clean
          architecture principles and modern development practices. I'm
          passionate about writing maintainable Python code,
          <em>building scalable backend systems</em>,
          <em>improving UI/UX flows</em>, and creating applications that feel
          fast, secure, and intuitive. I actively explore modern tools and
          technologies in the Python ecosystem to stay updated and
          continuously improve my development workflow.
        </p>

        <button class="btn-download">Download CV</button>
      </div>
    </section>

    <!-- ===================== SKILLS ===================== -->
    <section id="skills" class="skills-wrapper">
      <h2 class="section-title">Skills &amp; Technologies</h2>

      <div class="skills-grid">
        <div class="skill-card" v-for="skill in skills" :key="skill.name">
          <div class="skill-icon" v-html="skill.icon"></div>
          <p class="skill-name">{{ skill.name }}</p>
        </div>
      </div>
    </section>

    <!-- ===================== PROJECTS ===================== -->
    <section id="projects" class="projects-wrapper">
      <h2 class="section-title">Projects</h2>

      <div class="projects-grid">
        <div class="project-card" v-for="project in projects" :key="project.title">
          <img
            :src="project.image"
            :alt="project.title"
            class="project-image"
          />
          <div class="project-body">
            <h3 class="project-title">{{ project.title }}</h3>
            <p class="project-description">{{ project.description }}</p>
            <div class="tag-list">
              <span class="tag" v-for="tag in project.tags" :key="tag">{{ tag }}</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- ===================== CONTACT ===================== -->
    <section id="contact" class="contact-wrapper">
      <div class="contact-grid">
        <div class="contact-left">
          <h2 class="contact-title">Get In Touch</h2>
          <p class="contact-subtitle">
            I'd love to hear about your next project or collaboration. Send
            me a message and I'll get back to you within 24 hours.
          </p>

          <form class="contact-form" @submit.prevent="handleSubmit">
            <div class="form-row">
              <div class="form-group">
                <label>Name</label>
                <input
                  type="text"
                  placeholder="Your name"
                  v-model="form.name"
                  required
                />
              </div>
              <div class="form-group">
                <label>Email</label>
                <input
                  type="email"
                  placeholder="you@email.com"
                  v-model="form.email"
                  required
                />
              </div>
            </div>

            <div class="form-group">
              <label>Subject</label>
              <input
                type="text"
                placeholder="Briefly describe your inquiry"
                v-model="form.subject"
                required
              />
            </div>

            <div class="form-group">
              <label>Message</label>
              <textarea
                rows="4"
                placeholder="How can I help?"
                v-model="form.message"
                required
              ></textarea>
            </div>

            <button type="submit" class="btn-send" :disabled="isSubmitting">
              {{ isSubmitting ? "Sending..." : "Send Message" }}
            </button>

            <p v-if="statusMessage" :class="['form-status', statusType]">
              {{ statusMessage }}
            </p>
          </form>

          <div class="social-block">
            <p class="social-label">Social</p>
            <div class="social-icons">
              <a href="#" class="social-icon" aria-label="GitHub" v-html="icons.github"></a>
              <a href="#" class="social-icon" aria-label="LinkedIn" v-html="icons.linkedin"></a>
              <a href="#" class="social-icon" aria-label="Twitter" v-html="icons.twitter"></a>
            </div>
          </div>
        </div>

        <div class="contact-right">
          <div class="info-card">
            <h3 class="info-title">Contact Info</h3>
            <ul class="info-list">
              <li>
                <span class="info-icon" v-html="icons.mail"></span>
                prawinj3@gmail.com
              </li>
              <li>
                <span class="info-icon" v-html="icons.phone"></span>
                +91 99409 80625
              </li>
              <li>
                <span class="info-icon" v-html="icons.pin"></span>
                Tamil Nadu, India
              </li>
            </ul>
          </div>

          <div class="quote-card">
            <p class="quote-text">
              Whether it's a new project, a collaboration, or just a chat
              about code - I'm here to help. Let's build something amazing
              together.
            </p>
            <p class="quote-signature">- Prawin Kumar</p>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue'
import profileImage from './assets/Gemini_Generated_Image_4oad6p4oad6p4oad-removebg-preview.png'
import image1 from './assets/image 1.png'
import image2 from './assets/image 2.png'
import image3 from './assets/image 3.png'
import psql from './assets/psql.jpg'

const mobileMenuOpen = ref(false)

const toggleMenu = () => {
  mobileMenuOpen.value = !mobileMenuOpen.value
}

const closeMenu = () => {
  mobileMenuOpen.value = false
}

/* ===================== CONTACT FORM ===================== */

// Point this at your FastAPI backend (adjust host/port/path for your deployment)
const API_BASE_URL = 'http://localhost:8000'

const form = reactive({
  name: '',
  email: '',
  subject: '',
  message: '',
})

const isSubmitting = ref(false)
const statusMessage = ref('')
const statusType = ref('') // 'success' | 'error'

const resetForm = () => {
  form.name = ''
  form.email = ''
  form.subject = ''
  form.message = ''
}

const handleSubmit = async () => {
  statusMessage.value = ''
  statusType.value = ''
  isSubmitting.value = true

  try {
    const response = await fetch(`${API_BASE_URL}/api/contact`, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ ...form }),
    })

    const data = await response.json().catch(() => ({}))

    if (!response.ok) {
      throw new Error(data.detail || 'Something went wrong. Please try again.')
    }

    statusType.value = 'success'
    statusMessage.value = data.message || 'Thanks! Your message has been sent.'
    resetForm()
  } catch (err) {
    statusType.value = 'error'
    statusMessage.value = err.message || 'Failed to send message. Please try again later.'
  } finally {
    isSubmitting.value = false
  }
}

const skills = [
  {
    name: "Python",
    icon: `<svg viewBox="0 0 32 32" width="40" height="40"><path fill="#3776AB" d="M15.9 2c-1.4 0-2.7.1-3.8.3-3.4.6-4 1.9-4 4.2v3.1h8v1H8.1c-2.3 0-4.4 1.4-5 4-.7 3-.8 4.9 0 8 .6 2.4 2.1 4 4.4 4h2.8v-3.7c0-2.6 2.3-4.9 5-4.9h8c2.2 0 4-1.8 4-4V6.5c0-2.2-1.8-3.9-4-4.2C21.6 2.1 18.7 2 15.9 2zm-4.3 2.4c.8 0 1.5.7 1.5 1.6 0 .9-.7 1.6-1.5 1.6-.8 0-1.5-.7-1.5-1.6 0-.9.7-1.6 1.5-1.6z"/><path fill="#FFD43B" d="M16.1 30c1.4 0 2.7-.1 3.8-.3 3.4-.6 4-1.9 4-4.2v-3.1h-8v-1h11.9c2.3 0 4.4-1.4 5-4 .7-3 .8-4.9 0-8-.6-2.4-2.1-4-4.4-4h-2.8v3.7c0 2.6-2.3 4.9-5 4.9h-8c-2.2 0-4 1.8-4 4v6.7c0 2.2 1.8 3.9 4 4.2 1.2.1 4.1.1 4.5.1zm4.3-2.4c-.8 0-1.5-.7-1.5-1.6 0-.9.7-1.6 1.5-1.6.8 0 1.5.7 1.5 1.6 0 .9-.7 1.6-1.5 1.6z"/></svg>`,
  },
  {
    name: "React Js",
    icon: `<svg viewBox="0 0 32 32" width="40" height="40" fill="none" stroke="#61DAFB" stroke-width="1.2"><circle cx="16" cy="16" r="2.5" fill="#61DAFB" stroke="none"/><ellipse cx="16" cy="16" rx="12" ry="5"/><ellipse cx="16" cy="16" rx="12" ry="5" transform="rotate(60 16 16)"/><ellipse cx="16" cy="16" rx="12" ry="5" transform="rotate(120 16 16)"/></svg>`,
  },
  {
    name: "Vue Js",
    icon: `<svg viewBox="0 0 32 32" width="40" height="40"><path fill="#41B883" d="M2 4h5.5L16 18l8.5-14H30L16 28 2 4z"/><path fill="#35495E" d="M7.5 4h4.4L16 11l4.1-7h4.4L16 18 7.5 4z"/></svg>`,
  },
  {
    name: "FastAPI",
    icon: `<svg viewBox="0 0 32 32" width="40" height="40"><circle cx="16" cy="16" r="14" fill="#009688"/><path fill="#fff" d="M17.5 5 8 17h6.5l-2 10L24 15h-6.5l0-10z"/></svg>`,
  },
  {
    name: "Django",
    icon: `<svg viewBox="0 0 32 32" width="40" height="40"><circle cx="16" cy="16" r="14" fill="#092E20"/><text x="16" y="21" font-size="14" font-weight="700" fill="#0C4B33" text-anchor="middle" font-family="Georgia, serif">dj</text></svg>`,
  },
  {
    name: "PostgreSQL",
    icon: `<img src="${psql}" width="100" height="50" style="object-fit:contain;border-radius:6px;" />`
  }
];

const projects = [
  {
    title: "Employee Management System",
    description:
      "A full-stack application for managing employee records, attendance, and performance tracking.",
    tags: ["Vue.JS", "FastAPI", "PostgreSQL"],
    image: image1,
  },
  {
    title: "RAG Application",
    description:
      "A Retrieval-Augmented Generation app that combines document retrieval with AI-powered responses for intelligent Q&A.",
    tags: ["Vue.JS", "LangChain", "FastAPI"],
    image: image2,
  },
  {
    title: "Voice to Text Converter",
    description:
      "A real-time speech recognition tool that converts spoken audio into accurate written text.",
    tags: ["Vue.JS", "Whisper API", "FastAPI"],
    image: image3,
  },
];

const icons = {
  github: `<svg viewBox="0 0 24 24" width="18" height="18" fill="currentColor"><path d="M12 .5C5.65.5.5 5.65.5 12c0 5.09 3.29 9.4 7.86 10.93.57.1.78-.25.78-.55v-2.15c-3.2.7-3.87-1.36-3.87-1.36-.53-1.34-1.29-1.7-1.29-1.7-1.05-.72.08-.7.08-.7 1.16.08 1.78 1.2 1.78 1.2 1.03 1.76 2.7 1.25 3.36.96.1-.75.4-1.25.73-1.54-2.56-.29-5.25-1.28-5.25-5.7 0-1.26.45-2.29 1.19-3.09-.12-.29-.52-1.47.11-3.06 0 0 .97-.31 3.18 1.18a11 11 0 0 1 5.8 0c2.2-1.49 3.17-1.18 3.17-1.18.63 1.59.23 2.77.12 3.06.74.8 1.18 1.83 1.18 3.09 0 4.43-2.7 5.4-5.27 5.69.42.36.78 1.08.78 2.18v3.23c0 .3.2.66.79.55A11.5 11.5 0 0 0 23.5 12C23.5 5.65 18.35.5 12 .5Z"/></svg>`,
  linkedin: `<svg viewBox="0 0 24 24" width="18" height="18" fill="currentColor"><path d="M20.45 20.45h-3.55v-5.57c0-1.33-.02-3.03-1.85-3.03-1.85 0-2.14 1.45-2.14 2.94v5.66H9.36V9h3.41v1.56h.05c.47-.9 1.63-1.85 3.36-1.85 3.6 0 4.27 2.37 4.27 5.45v6.29ZM5.34 7.43a2.06 2.06 0 1 1 0-4.12 2.06 2.06 0 0 1 0 4.12ZM7.12 20.45H3.56V9h3.56v11.45Z"/></svg>`,
  twitter: `<svg viewBox="0 0 24 24" width="18" height="18" fill="currentColor"><path d="M22 5.9c-.7.3-1.5.5-2.3.6.8-.5 1.5-1.3 1.8-2.3-.8.5-1.7.8-2.6 1a4.1 4.1 0 0 0-7 3.7A11.6 11.6 0 0 1 3.4 4.6a4.1 4.1 0 0 0 1.3 5.4c-.6 0-1.3-.2-1.8-.5v.1c0 2 1.4 3.6 3.3 4a4.1 4.1 0 0 1-1.8.1c.5 1.6 2 2.8 3.8 2.8A8.2 8.2 0 0 1 2 18.6a11.6 11.6 0 0 0 6.3 1.8c7.5 0 11.7-6.3 11.7-11.7v-.5c.8-.6 1.5-1.3 2-2.1Z"/></svg>`,
  mail: `<svg viewBox="0 0 24 24" width="16" height="16" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="5" width="18" height="14" rx="2"/><path d="m3 7 9 6 9-6"/></svg>`,
  phone: `<svg viewBox="0 0 24 24" width="16" height="16" fill="none" stroke="currentColor" stroke-width="2"><path d="M22 16.9v3a2 2 0 0 1-2.2 2 19.8 19.8 0 0 1-8.6-3.1 19.5 19.5 0 0 1-6-6A19.8 19.8 0 0 1 2.1 4.2 2 2 0 0 1 4 2h3a2 2 0 0 1 2 1.7c.1.9.3 1.8.6 2.7a2 2 0 0 1-.4 2.1L8 9.9a16 16 0 0 0 6 6l1.4-1.4a2 2 0 0 1 2.1-.4c.9.3 1.8.5 2.7.6a2 2 0 0 1 1.8 2.2Z"/></svg>`,
  pin: `<svg viewBox="0 0 24 24" width="16" height="16" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 10c0 6-9 12-9 12s-9-6-9-12a9 9 0 0 1 18 0Z"/><circle cx="12" cy="10" r="3"/></svg>`,
};
</script>

<style scoped>
* {
  box-sizing: border-box;
}

#app {
  background-color: #0a0a0a;
  color: #ffffff;
  font-family: "Segoe UI", "Helvetica Neue", Arial, sans-serif;
  overflow-x: hidden;
}

.accent {
  color: #6c5ce7;
}

/* ===================== NAVBAR ===================== */
.navbar {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 24px 60px;
}

.logo {
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: 22px;
  font-weight: 700;
  white-space: nowrap;
}

.logo-bracket {
  color: #6c5ce7;
}

.nav-links {
  display: flex;
  list-style: none;
  gap: 40px;
  margin: 0;
  padding: 0;
}

.nav-links a {
  color: #ffffff;
  text-decoration: none;
  font-size: 16px;
  font-weight: 500;
  transition: color 0.2s ease;
}

.nav-links a:hover {
  color: #6c5ce7;
}

/* Navbar right-side actions (CV button + hamburger) */
.navbar-actions {
  display: flex;
  align-items: center;
  gap: 20px;
}

/* Hamburger toggle (hidden on desktop) */
.hamburger {
  display: none;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 5px;
  width: 34px;
  height: 34px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 0;
  z-index: 1001;
}

.hamburger span {
  display: block;
  width: 24px;
  height: 2px;
  background-color: #ffffff;
  border-radius: 2px;
  transition: transform 0.25s ease, opacity 0.25s ease;
}

.hamburger.active span:nth-child(1) {
  transform: translateY(7px) rotate(45deg);
}

.hamburger.active span:nth-child(2) {
  opacity: 0;
}

.hamburger.active span:nth-child(3) {
  transform: translateY(-7px) rotate(-45deg);
}

/* Backdrop shown behind the mobile menu */
.nav-backdrop {
  display: none;
}

/* Buttons (shared) */
.btn {
  cursor: pointer;
  font-size: 16px;
  font-weight: 700;
  border-radius: 6px;
  padding: 12px 28px;
  border: 2px solid transparent;
  transition: all 0.2s ease;
}

.btn-primary {
  background-color: #6c5ce7;
  color: #ffffff;
  display: inline-flex;
  align-items: center;
  gap: 10px;
}

.btn-primary:hover {
  background-color: #5a4bd1;
}

.btn-outline {
  background-color: transparent;
  border-color: #6c5ce7;
  color: #ffffff;
}

.btn-outline:hover {
  background-color: rgba(108, 92, 231, 0.1);
}

.download-btn {
  padding: 10px 24px;
  font-size: 15px;
}

.arrow {
  font-size: 18px;
}

/* ===================== HERO ===================== */
.hero {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 60px 60px 100px;
  gap: 40px;
}

.hero-text {
  flex: 1;
  max-width: 650px;
  z-index: 2;
}

.hero-title {
  font-size: 64px;
  font-weight: 800;
  line-height: 1.1;
  margin: 0 0 10px;
}

.hero-subtitle {
  font-size: 34px;
  font-weight: 700;
  margin: 0 0 24px;
}

.hero-description {
  font-size: 17px;
  line-height: 1.6;
  color: #d0d0d0;
  margin: 0 0 36px;
  max-width: 500px;
}

.hero-buttons {
  display: flex;
  gap: 16px;
}

.hero-image {
  position: relative;
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  max-width: 450px;
}

.image-circle {
  margin-top: 80px;
  margin-left: -30px;
  position: absolute;
  width: 340px;
  height: 340px;
  background-color: #6c5ce7;
  border-radius: 50%;
  z-index: 1;
}

.profile-img {
  position: relative;
  z-index: 2;
  height: 500px;
  width: 600px;
  border-radius: 12px;
  object-fit: cover;
  display: block;
}

/* ===================== ABOUT ===================== */
.about-wrapper {
  display: flex;
  align-items: center;
  gap: 60px;
  padding: 80px 60px;
}

.about-image {
  flex: 0 0 auto;
}

.image-card {
  width: 340px;
  height: 440px;
  background-color: #6c5ce7;
  border-radius: 32px;
  overflow: hidden;
  display: flex;
  align-items: flex-end;
  justify-content: center;
}

.about-profile-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.about-text {
  flex: 1;
  max-width: 560px;
}

.about-title {
  font-size: 42px;
  font-weight: 800;
  margin: 0 0 28px;
}

.about-paragraph {
  font-size: 16px;
  line-height: 1.7;
  color: #e0e0e0;
  margin: 0 0 20px;
}

.about-paragraph em {
  font-style: italic;
  color: #ffffff;
}

.btn-download {
  margin-top: 12px;
  background-color: #6c5ce7;
  color: #ffffff;
  border: none;
  border-radius: 8px;
  padding: 14px 30px;
  font-size: 16px;
  font-weight: 700;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.btn-download:hover {
  background-color: #5a4bd1;
}

/* ===================== SECTION TITLE (shared) ===================== */
.section-title {
  text-align: center;
  font-size: 40px;
  font-weight: 800;
  margin: 0 0 60px;
}

/* ===================== SKILLS ===================== */
.skills-wrapper {
  padding: 80px 60px;
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 220px));
  gap: 30px;
  justify-content: center;
}

.skill-card {
  border: 1.5px solid #6c5ce7;
  border-radius: 14px;
  padding: 40px 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 20px;
  background-color: #0a0a0a;
  box-shadow: 0 0 18px rgba(108, 92, 231, 0.15);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.skill-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 0 26px rgba(108, 92, 231, 0.35);
}

.skill-icon {
  display: flex;
  align-items: center;
  justify-content: center;
}

.skill-name {
  font-size: 18px;
  font-weight: 700;
  margin: 0;
}

/* ===================== PROJECTS ===================== */
.projects-wrapper {
  padding: 80px 60px 100px;
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 28px;
  max-width: 1200px;
  margin: 0 auto;
}

.project-card {
  background-color: #131313;
  border-radius: 12px;
  overflow: hidden;
  border: 1px solid #222;
}

.project-image {
  height: 170px;
  width: 100%;
  object-fit: cover;
  display: block;
}

.project-body {
  padding: 20px;
}

.project-title {
  font-size: 19px;
  font-weight: 700;
  margin: 0 0 10px;
}

.project-description {
  font-size: 14px;
  line-height: 1.55;
  color: #b8b8b8;
  margin: 0 0 18px;
}

.tag-list {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.tag {
  background-color: #232323;
  color: #d8d8d8;
  font-size: 12px;
  font-weight: 600;
  padding: 5px 12px;
  border-radius: 6px;
}

/* ===================== CONTACT ===================== */
.contact-wrapper {
  padding: 80px 60px 100px;
}

.contact-grid {
  display: grid;
  grid-template-columns: 1.5fr 1fr;
  gap: 40px;
  max-width: 1200px;
  margin: 0 auto;
}

.contact-title {
  font-size: 40px;
  font-weight: 800;
  margin: 0 0 14px;
}

.contact-subtitle {
  font-size: 15px;
  line-height: 1.6;
  color: #b8b8b8;
  max-width: 480px;
  margin: 0 0 28px;
}

.contact-form {
  background-color: #131313;
  border: 1px solid #222;
  border-radius: 14px;
  padding: 28px;
  display: flex;
  flex-direction: column;
  gap: 18px;
}

.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 16px;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.form-group label {
  font-size: 13px;
  font-weight: 700;
  color: #e0e0e0;
}

.form-group input,
.form-group textarea {
  background-color: #0a0a0a;
  border: 1px solid #2c2c2c;
  border-radius: 8px;
  padding: 12px 14px;
  color: #ffffff;
  font-size: 14px;
  font-family: inherit;
  resize: none;
  outline: none;
  transition: border-color 0.2s ease;
}

.form-group input:focus,
.form-group textarea:focus {
  border-color: #6c5ce7;
}

.form-group input::placeholder,
.form-group textarea::placeholder {
  color: #6f6f6f;
}

.btn-send {
  background-color: #6c5ce7;
  color: #ffffff;
  border: none;
  border-radius: 8px;
  padding: 14px;
  font-size: 15px;
  font-weight: 700;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.btn-send:hover {
  background-color: #5a4bd1;
}

.btn-send:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.form-status {
  margin: 0;
  font-size: 14px;
  font-weight: 600;
  text-align: center;
}

.form-status.success {
  color: #4ade80;
}

.form-status.error {
  color: #f87171;
}

.social-block {
  margin-top: 28px;
}

.social-label {
  font-size: 14px;
  font-weight: 700;
  margin: 0 0 12px;
}

.social-icons {
  display: flex;
  gap: 12px;
}

.social-icon {
  width: 38px;
  height: 38px;
  border-radius: 8px;
  background-color: #1a1a2e;
  color: #8a7dfa;
  display: flex;
  align-items: center;
  justify-content: center;
  text-decoration: none;
  transition: background-color 0.2s ease;
}

.social-icon:hover {
  background-color: #26264a;
}

/* Contact right column */
.contact-right {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.info-card,
.quote-card {
  background-color: #131313;
  border: 1px solid #222;
  border-radius: 14px;
  padding: 24px;
}

.info-title {
  font-size: 20px;
  font-weight: 700;
  margin: 0 0 18px;
}

.info-list {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: column;
  gap: 14px;
}

.info-list li {
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 14px;
  color: #d8d8d8;
}

.info-icon {
  color: #8a7dfa;
  display: flex;
  align-items: center;
}

.quote-text {
  font-size: 14px;
  line-height: 1.6;
  color: #cfcfcf;
  margin: 0 0 14px;
}

.quote-signature {
  font-size: 14px;
  font-weight: 700;
  color: #8a7dfa;
  margin: 0;
}

/* ===================== RESPONSIVE ===================== */

/* Tablet / mobile navbar: switch to hamburger + slide-in drawer */
@media (max-width: 768px) {
  .navbar {
    padding: 20px 24px;
  }

  .about-image{
    display: none;
  }

  .hamburger {
    display: flex;
  }

  .download-btn {
    display: none;
  }

  .nav-links {
    position: fixed;
    top: 0;
    right: 0;
    height: 100vh;
    width: min(78vw, 300px);
    background-color: #0f0f0f;
    flex-direction: column;
    align-items: flex-start;
    gap: 4px;
    margin: 0;
    padding: 90px 30px 30px;
    transform: translateX(100%);
    transition: transform 0.3s ease;
    box-shadow: -10px 0 30px rgba(0, 0, 0, 0.5);
    z-index: 1000;
  }

  .nav-links.nav-links-open {
    transform: translateX(0);
  }

  .nav-links li {
    width: 100%;
  }

  .nav-links a {
    display: block;
    width: 100%;
    padding: 14px 0;
    font-size: 18px;
    border-bottom: 1px solid #222;
  }

  .nav-backdrop {
    display: block;
    position: fixed;
    inset: 0;
    background-color: rgba(0, 0, 0, 0.6);
    z-index: 999;
  }
}

@media (max-width: 992px) {
  .hero {
    flex-direction: column;
    text-align: center;
    padding: 40px 30px 60px;
  }

  .hero-text {
    max-width: 100%;
  }

  .hero-description {
    margin-left: auto;
    margin-right: auto;
  }

  .hero-buttons {
    justify-content: center;
  }

  .about-wrapper {
    flex-direction: column;
    text-align: center;
    padding: 60px 30px;
  }

  .about-text {
    max-width: 100%;
  }

  .skills-wrapper,
  .projects-wrapper,
  .contact-wrapper {
    padding: 60px 30px;
  }

  .skills-grid {
    grid-template-columns: repeat(2, minmax(0, 220px));
  }

  .projects-grid {
    grid-template-columns: 1fr;
  }

  .contact-grid {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 480px) {
  .hero-title {
    font-size: 36px;
  }

  .profile-img,
  .image-circle {
    width: 260px;
    height: 260px;
  }
  .about-image{
    display: none;
  }

  .image-card img {
    display: none;
    width: 220px;
    height: 300px;
    border-radius: 24px;
  }
  .about-title,
  .contact-title,
  .section-title {
    font-size: 30px;
  }


  .skills-grid {
    grid-template-columns: 1fr;
  }

  .form-row {
    grid-template-columns: 1fr;
  }
}
</style>