### Setting up the Portfolio

Ubuntu Server Setup

Nginx Setup

Tailscale Setup

[Porfolio Link](https://marsnts.tarsier-map.ts.net/)

All files should be in the `/www/var/<foldername>`
#### index.html
```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta name="description" content="DevOps engineering portfolio showcasing infrastructure, automation, CI/CD, and homelab projects.">
  <title>MARSNTS — Aspiring DevOps Engineer</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=DM+Mono:wght@400;500&family=DM+Sans:wght@400;500;600;700&family=Manrope:wght@400;500;600;700;800&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="styles.css">
  <script src="script.js" defer></script>
</head>

  <link rel="stylesheet" href="style.css">
  <script src="script.js" defer></script>
  
<link rel="stylesheet" href="styles.css">
<link rel="icon" type="image/png" href="assets/favicon.png">
</head>
<body>
  <div class="topline"><span><i class="pulse"></i> OPEN TO JUNIOR / ENTRY-LEVEL OPPORTUNITIES</span><span class="topline-right">MANILA, PHILIPPINES <b>·</b> UTC+8 
</button></span></div>
  <header class="site-header" id="top">
    <a class="brand" href="#home"><span class="brand-icon">
      <img
        class="brand-logo"
        src="assets/favicon.png"
        alt="MARSNTS"
        width="34"
        height="34"
      >
  </span>
  <span>MARSNTS<span class="brand-muted"> / portfolio</span></span></a>
    <button class="menu-toggle" aria-label="Toggle navigation" aria-expanded="false"><span></span><span></span></button>
    <nav class="nav" aria-label="Main navigation">
      <a class="nav-link active" href="#home">Overview</a>
      <a class="nav-link" href="#stack">Tech stack</a>
      <a class="nav-link" href="#projects">Projects</a>
      <a class="nav-link" href="#journey">Journey</a>
      <a class="nav-link nav-contact" href="#contact">Contact <span>↗</span></a>
    <a>
    <button
    class="theme-toggle"
    id="theme-toggle"
    type="button"
    aria-label="Switch to dark mode"
    aria-pressed="false"
>
    <svg class="theme-icon theme-icon-moon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
        <path d="M20.9 13.3A9 9 0 0 1 10.7 3.1a9 9 0 1 0 10.2 10.2Z"/>
    </svg>

    <svg class="theme-icon theme-icon-sun" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7" stroke-linecap="round" aria-hidden="true">
        <circle cx="12" cy="12" r="4"/>
        <path d="M12 2v2 M12 20v2 M2 12h2 M20 12h2 M4.93 4.93l1.42 1.42 M17.65 17.65l1.42 1.42 M4.93 19.07l1.42-1.42 M17.65 6.35l1.42-1.42"/>
    </svg>
</button>
</a>
</nav>
  </header>

  <main>
    <section class="hero section-wrap" id="home">
      <div class="hero-copy">
        <p class="eyebrow"><span class="terminal-mark">~/</span> INTRODUCTION</p>
        <h1>Building reliable systems.<br><span class="hero-accent">Automating the repeatable.</span></h1>
        <p class="hero-intro">I'm Mar, an aspiring DevOps Engineer focused on Linux, infrastructure, automation, and the tools that help software ship reliably.</p>
        <div class="hero-actions">
          <a class="button button-primary" href="#projects">Explore my projects <span>↓</span></a>
          <a class="text-link" href="https://github.com/marsnts" target="_blank" rel="noreferrer">View GitHub <span>↗</span></a>
        </div>
        <div class="hero-facts">
          <div><span class="fact-label">CURRENT FOCUS</span><strong>Linux · Networking · Self-hosting</strong></div>
          <div><span class="fact-label">CAREER GOAL</span><strong>Junior DevOps / Network Engineer</strong></div>
        </div>
      </div>
      <div class="terminal-wrap" aria-label="Decorative terminal showing DevOps learning themes">
        <div class="terminal-window">
          <div class="terminal-titlebar"><div class="window-dots"><i></i><i></i><i></i></div><span>mar@homelab: ~/portfolio</span><span class="terminal-lock">● LOCAL</span></div>
          <div class="terminal-body">
            <p><span class="term-muted"># what I'm working toward</span></p>
            <p><span class="term-green">mar@homelab</span><span class="term-muted">:</span><span class="term-blue">~</span><span>$</span> whoami</p>
            <p class="term-output">aspiring-devops-engineer</p>
            <p><span class="term-green">mar@homelab</span><span class="term-muted">:</span><span class="term-blue">~</span><span>$</span> cat focus.txt</p>
            <p class="term-output">linux<br>automation<br>networking<br>ci-cd<br>observability</p>
            <p><span class="term-green">mar@homelab</span><span class="term-muted">:</span><span class="term-blue">~</span><span>$</span> <span class="cursor"></span></p>
          </div>
          <div class="terminal-status"><span><i class="status-dot"></i> LEARNING IN PROGRESS</span><span>UTF-8 <b>·</b> bash</span></div>
        </div>
        <div class="terminal-chip chip-top"><span>⌘</span> Infrastructure as Code</div>
        <div class="terminal-chip chip-bottom"><span>↻</span> Automate · Deploy · Improve</div>
        <div class="hero-grid-decoration"></div>
      </div>
      <a class="scroll-cue" href="#about"><span></span> SCROLL TO EXPLORE</a>
    </section>

    <section class="signal-strip"><div class="section-wrap signal-inner"><span>LEARN</span><b>→</b><span>BUILD</span><b>→</b><span>AUTOMATE</span><b>→</b><span>MONITOR</span><b>→</b><span>IMPROVE</span></div></section>

    <section class="section section-wrap" id="about">
      <div class="section-heading"><p class="eyebrow">01 / PROFILE</p><span class="section-number">ABOUT</span></div>
      <div class="about-grid">
        <h2>From running commands<br>to <span class="serif-accent">understanding systems.</span></h2>
        <div class="about-copy">
          <p class="lead">I'm developing practical skills in Linux administration, networking, deployment, and infrastructure operations through hands-on projects.</p>
          <p>I enjoy learning how services fit together: how a server gets online, how traffic reaches an application, how deployments can be repeated, and how systems can be monitored and maintained. My goal is to grow into a DevOps Engineer who makes delivery more dependable and operations less manual.</p>
          <a class="text-link underlined" href="#journey">See my learning roadmap <span>↘</span></a>
        </div>
      </div>
      <div class="principles">
        <article><span class="principle-icon">01</span><h3>Infrastructure fundamentals</h3><p>Linux, networking, virtual machines, services, and troubleshooting.</p></article>
        <article><span class="principle-icon">02</span><h3>Automation mindset</h3><p>Use scripts and repeatable configuration to reduce manual work.</p></article>
        <article><span class="principle-icon">03</span><h3>Document everything</h3><p>Keep projects reproducible with Git, clear READMEs, and diagrams.</p></article>
      </div>
    </section>

    <section class="stack-section" id="stack">
      <div class="section section-wrap">
        <div class="section-heading"><p class="eyebrow">02 / TOOLS & TECHNOLOGIES</p><span class="section-number">TECH STACK</span></div>
        <div class="stack-heading"><h2>Tools I'm learning<br>to <span class="serif-accent">put to work.</span></h2><p>My current stack is a work in progress. I separate hands-on experience from technologies on my learning roadmap.</p></div>
        <div class="stack-grid">
          <article class="stack-card"><div class="stack-card-top"><span class="stack-icon">01</span><span class="roadmap-check">●</span></div><h3>Systems & virtualization</h3><div class="tag-list"><span>Linux</span><span>Ubuntu Server</span><span>Proxmox VE</span><span>VMware</span></div><p>Server setup, virtual machines, system services, and host management.</p><span class="stack-status status-practicing">HANDS-ON FOCUS</span></article>
          <article class="stack-card"><div class="stack-card-top"><span class="stack-icon">02</span><span class="roadmap-check">●</span></div><h3>Networking & delivery</h3><div class="tag-list"><span>TCP/IP</span><span>DNS</span><span>Nginx</span><span>Tailscale</span></div><p>Understand connectivity, reverse proxies, DNS, and secure service exposure.</p><span class="stack-status status-practicing">HANDS-ON FOCUS</span></article>
          <article class="stack-card"><div class="stack-card-top"><span class="stack-icon">03</span><span class="roadmap-check">●</span></div><h3>Code & version control</h3><div class="tag-list"><span>Python</span><span>Bash</span><span>Git</span><span>GitHub</span></div><p>Write small tools, track changes, and document projects in version control.</p><span class="stack-status status-practicing">BUILDING SKILLS</span></article>
          <article class="stack-card"><div class="stack-card-top"><span class="stack-icon">04</span><span class="roadmap-check">●</span></div><h3>Technical Support</h3><div class="tag-list"><span>Ticket Management</span><span>Inventory Management</span><span>Hardware and Software Optimization</span></div><p>Build a pipeline, manage infrastructure as code, and add logs and metrics.</p><span class="stack-status status-practicing">COMMUNICATION AND DOCUMENTATION SKILLS</span></article>
          <article class="stack-card"><div class="stack-card-top"><span class="stack-icon">05</span><span class="roadmap-state">○</span></div><h3>Next on my roadmap</h3><div class="tag-list"><span>Docker</span><span>CI/CD</span><span>Terraform</span><span>Monitoring</span></div><p>Build a pipeline, manage infrastructure as code, and add logs and metrics.</p><span class="stack-status status-roadmap">LEARNING ROADMAP</span></article>
        </div>
        <p class="stack-note"></p>
      </div>
    </section>

    <section class="section section-wrap projects" id="projects">
      <div class="section-heading"><p class="eyebrow">03 / HANDS-ON WORK</p><span class="section-number">PROJECTS</span></div>
      <div class="projects-heading"><h2>Learning by<br><span class="serif-accent">building things.</span></h2><p>Projects are the proof. Each entry should explain the problem, the setup, what you did, and what you learned.</p></div>
      <div class="project-filters" role="group" aria-label="Filter projects">
        <button class="filter-button active" data-filter="all">All projects <span>03</span></button>
        <button class="filter-button" data-filter="infrastructure">Infrastructure</button>
        <button class="filter-button" data-filter="web">Web hosting</button>
        <button class="filter-button" data-filter="automation">Automation</button>
      </div>
      <div class="project-grid">
        <article class="project-card" data-category="infrastructure">
          <div class="project-art art-proxmox"><div class="diagram-node node-host"><span>▣</span><b>Proxmox VE</b><small>Physical host</small></div><div class="diagram-connector"></div><div class="diagram-vms"><div class="diagram-node"><span>▤</span><b>Ubuntu VM</b><small>Services</small></div><div class="diagram-node"><span>▤</span><b>Linux VM</b><small>Lab</small></div></div><span class="art-label">HOMELAB / 01</span></div>
          <div class="project-info"><div><p class="project-type">VIRTUALIZATION · LINUX · NETWORKING</p><h3>Proxmox Homelab</h3></div><span class="project-year">01</span></div>
          <p class="project-description">Set up a Proxmox VE host on repurposed laptop hardware, configured network access, and began troubleshooting connectivity for virtual machines.</p>
          <div class="project-outcomes"><span>Host configuration</span><span>Bridge networking</span><span>Troubleshooting</span></div>
          <a class="project-link" href="https://github.com/marsnts" target="_blank" rel="noreferrer">View project / notes <span>↗</span></a>
        </article>
        <article class="project-card" data-category="web">
          <div class="project-art art-nginx"><div class="browser-frame"><div class="browser-bar"><i></i><i></i><i></i><span>marsnts.com</span></div><div class="browser-content"><span class="browser-kicker">PERSONAL WEB SERVER</span><b>From local server<br>to public endpoint.</b><div class="browser-lines"><i></i><i></i><i></i></div><span class="browser-badge">HTTPS / TUNNEL</span></div></div><div class="web-stack"><span>Tailscale</span><b>↓</b><span>Nginx</span><b>↓</b><span>Static site</span></div><span class="art-label">SELF-HOSTING / 02</span></div>
          <div class="project-info"><div><p class="project-type">UBUNTU SERVER · NGINX · TAILSCALE</p><h3>Self-hosted Static Website</h3></div><span class="project-year">02</span></div>
          <p class="project-description">Build a static site on Ubuntu Server with Nginx and Tailscale, learning service configuration, ingress routing, and troubleshooting.</p>
          <div class="project-outcomes"><span>Linux services</span><span>Reverse proxy concepts</span><span>Tunnel configuration</span></div>
          <a class="project-link" href="#contact">Add repository / write-up <span>↗</span></a>
        </article>
        <article class="project-card" data-category="automation">
          <div class="project-art art-spotiflac"><div class="code-window"><div class="code-title"><i></i><i></i><i></i><span>download_manager.py</span></div><div class="code-lines"><p><em>class</em> <strong>DownloadManager</strong>:</p><p>　 <em>def</em> <strong>download</strong>(self, track):</p><p>　　 <b>provider</b> = self.select_provider()</p><p>　　 <b>return</b> provider.fetch(track)</p><p class="code-comment"># automate repetitive tasks</p></div></div><div class="code-stamp">PY<br>↻</div><span class="art-label">PYTHON / 03</span></div>
          <div class="project-info"><div><p class="project-type">PYTHON · GIT · API INTEGRATION</p><h3>Spoti-flac</h3></div><span class="project-year">03</span></div>
          <p class="project-description">Develop a Python GUI project that works with Spotify playlist data and download-provider components. Practice modular code, dependency management, and Git workflows.</p>
          <div class="project-outcomes"><span>Python application</span><span>Modular architecture</span><span>Git branching</span></div>
          <a class="project-link" href="https://github.com/marsnts/Spoti-flac" target="_blank" rel="noreferrer">View source on GitHub <span>↗</span></a>
        </article>
      </div>
      <p class="portfolio-note"></p>
    </section>

    <section class="roadmap-section" id="journey">
      <div class="section section-wrap">
        <div class="section-heading"><p class="eyebrow">04 / WHAT'S NEXT</p><span class="section-number">LEARNING ROADMAP</span></div>
        <div class="roadmap-heading"><h2>Progress over<br><span class="serif-accent">pretending.</span></h2><p>A practical plan to grow from foundational system administration into repeatable deployment and observability.</p></div>
        <div class="roadmap-list">
          <article><span class="roadmap-number">01</span><div><span class="roadmap-state">FOUNDATIONS</span><h3>Linux & networking</h3><p>Users and permissions, systemd, logs, SSH, DNS, routing, firewall rules, and troubleshooting.</p></div><span class="roadmap-check">●</span></article>
          <article><span class="roadmap-number">02</span><div><span class="roadmap-state">NEXT BUILD</span><h3>Containers & CI/CD</h3><p>Containerize a small app with Docker, then build a GitHub Actions pipeline to test and deploy it.</p></div><span class="roadmap-check roadmap-pending">○</span></article>
          <article><span class="roadmap-number">03</span><div><span class="roadmap-state">AFTER THAT</span><h3>Infrastructure as Code</h3><p>Use Terraform to provision reproducible infrastructure and keep configuration in version control.</p></div><span class="roadmap-check roadmap-pending">○</span></article>
          <article><span class="roadmap-number">04</span><div><span class="roadmap-state">LONG-TERM</span><h3>Observability & reliability</h3><p>Add metrics, dashboards, centralized logs, health checks, and a documented recovery process.</p></div><span class="roadmap-check roadmap-pending">○</span></article>
        </div>
      </div>
    </section>

    <section class="resume-section" id="journey">
      <div class="section section-wrap">
        <div class="section-heading"><p class="eyebrow">04 / WHAT'S NEXT</p><span class="section-number">LEARNING ROADMAP</span></div>
        <div class="roadmap-heading"><h2>Progress over<br><span class="serif-accent">pretending.</span></h2><p>A practical plan to grow from foundational system administration into repeatable deployment and observability.</p></div>
        <div class="roadmap-list">
          <article><span class="roadmap-number">01</span><div><span class="roadmap-state">FOUNDATIONS</span><h3>Linux & networking</h3><p>Users and permissions, systemd, logs, SSH, DNS, routing, firewall rules, and troubleshooting.</p></div><span class="roadmap-check">●</span></article>
          <article><span class="roadmap-number">02</span><div><span class="roadmap-state">NEXT BUILD</span><h3>Containers & CI/CD</h3><p>Containerize a small app with Docker, then build a GitHub Actions pipeline to test and deploy it.</p></div><span class="roadmap-check roadmap-pending">○</span></article>
          <article><span class="roadmap-number">03</span><div><span class="roadmap-state">AFTER THAT</span><h3>Infrastructure as Code</h3><p>Use Terraform to provision reproducible infrastructure and keep configuration in version control.</p></div><span class="roadmap-check roadmap-pending">○</span></article>
          <article><span class="roadmap-number">04</span><div><span class="roadmap-state">LONG-TERM</span><h3>Observability & reliability</h3><p>Add metrics, dashboards, centralized logs, health checks, and a documented recovery process.</p></div><span class="roadmap-check roadmap-pending">○</span></article>
        </div>
      </div>
    </section>

    <section class="stack-section" id="resume">
      <div class="section section-wrap">
        <div class="section-heading"><p class="eyebrow">05 / Professional Background</p><span class="section-number">RESUME</span></div>
        <div class="stack-heading"><h2>Where I've been.<br><span class="serif-accent">What I bring.</span></h2>
          
          <p>I am Martin Andrei Santos, a Licensed Electronics Engineer with experience in IT. I specialize in Technical Support and Networking, delivering continous uptime for clients. My work combines strong problem-solving skills, troubleshooting skills, communication skills, and a practical, results-focused approach.</p>
        
        </div>
        <a class="button button-secondary" href="">View Full Resume <span>↗</span></a>
        <p class="stack-note"></p>
      </div>
    </section>

    <section class="contact-section" id="contact">
      <div class="section section-wrap">
        <div class="section-heading"><p class="eyebrow">06 / GET IN TOUCH</p><span class="section-number">CONTACT</span></div>
        <div class="contact-grid"><div><h2>Let's build<br>something <span class="serif-accent">reliable.</span></h2><p class="contact-intro">I'm interested in junior DevOps, cloud, infrastructure, and system administration opportunities. I'm also happy to connect with people who enjoy building and learning.</p><a class="email-link" href="mailto:martinandreusantos@gmail.com">martinandreusantos@gmail.com <span>↗</span></a><div class="social-links"><a href="https://github.com/marsnts" target="_blank" rel="noreferrer">GitHub ↗</a><a href="https://www.linkedin.com/in/marsnts/" target="_blank" rel="noreferrer">LinkedIn ↗</a></div></div>
          <form class="contact-form" id="contact-form"><label for="name">NAME</label><input id="name" name="name" placeholder="Your name" required><label for="email">EMAIL</label><input id="email" name="email" type="email" placeholder="you@example.com" required><label for="message">MESSAGE</label><textarea id="message" name="message" rows="4" placeholder="What would you like to talk about?" required></textarea><button class="button button-primary" type="submit">Prepare email <span>↗</span></button><p class="form-note" id="form-note"></p></form>
        </div>
      </div>
    </section>
  </main>

  <footer class="footer"><div class="section-wrap footer-inner"><a class="brand" href="#top"><span class="brand-icon"><img
        class="brand-logo"
        src="assets/favicon.png"
        alt="MARSNTS"
        width="34"
        height="34"
      ></span><span>MARSNTS<span class="brand-muted"> / portfolio</span></span></a><p>Built with curiosity, documented with care.</p><div class="footer-links"><a href="#top">Back to top ↑</a><a href="https://github.com/marsnts" target="_blank" rel="noreferrer">GitHub ↗</a></div><span class="copyright">© <span id="year"></span> MARSNTS</span></div></footer>
</body>
</html>

```

#### script.js
```javascript
const menuToggle = document.querySelector(".menu-toggle");
const nav = document.querySelector(".nav");

menuToggle.addEventListener("click", () => {
  const isOpen = nav.classList.toggle("open");
  menuToggle.setAttribute("aria-expanded", String(isOpen));
});

document.querySelectorAll(".nav-link").forEach((link) => {
  link.addEventListener("click", () => {
    nav.classList.remove("open");
    menuToggle.setAttribute("aria-expanded", "false");
  });
});

const sections = [...document.querySelectorAll("main section[id]")];
const navLinks = [...document.querySelectorAll(".nav-link")];
if ("IntersectionObserver" in window) {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        navLinks.forEach((link) => {
          link.classList.toggle("active", link.getAttribute("href") === `#${entry.target.id}`);
        });
      }
    });
  }, { rootMargin: "-35% 0px -55% 0px" });
  sections.forEach((section) => observer.observe(section));
}

document.querySelectorAll(".filter-button").forEach((button) => {
  button.addEventListener("click", () => {
    const filter = button.dataset.filter;
    document.querySelectorAll(".filter-button").forEach((item) => item.classList.toggle("active", item === button));
    document.querySelectorAll(".project-card").forEach((card) => {
      card.hidden = filter !== "all" && card.dataset.category !== filter;
    });
  });
});

document.querySelector("#year").textContent = new Date().getFullYear();

document.querySelector("#contact-form").addEventListener("submit", (event) => {
  event.preventDefault();
  const form = new FormData(event.currentTarget);
  const name = String(form.get("name")).trim();
  const email = String(form.get("email")).trim();
  const message = String(form.get("message")).trim();
  const subject = encodeURIComponent(`Portfolio inquiry from ${name}`);
  const body = encodeURIComponent(`Hi Mar,\n\n${message}\n\nFrom: ${name}\nEmail: ${email}`);
  window.location.href = `mailto:YOUR_EMAIL@example.com?subject=${subject}&body=${body}`;
  document.querySelector("#form-note").textContent = "Your email app should open with a prepared draft. Replace YOUR_EMAIL@example.com with your real email address before publishing.";
});
(function () {
    const root = document.documentElement;
    const button = document.getElementById("theme-toggle");

    if (!button) {
        console.warn("Theme toggle button not found.");
        return;
    }

    const systemTheme = window.matchMedia("(prefers-color-scheme: dark)");
    let savedTheme = null;

    try {
        savedTheme = localStorage.getItem("theme");
    } catch (error) {
        console.warn("localStorage unavailable.");
    }

    const hasUserPreference =
        savedTheme === "light" || savedTheme === "dark";

    function applyTheme(theme) {
        const isDark = theme === "dark";

        root.dataset.theme = theme;
        button.setAttribute("aria-pressed", String(isDark));
        button.setAttribute(
            "aria-label",
            isDark ? "Switch to light mode" : "Switch to dark mode"
        );
        button.title = isDark
            ? "Switch to light mode"
            : "Switch to dark mode";
    }

    applyTheme(
        hasUserPreference
            ? savedTheme
            : systemTheme.matches
                ? "dark"
                : "light"
    );

    button.addEventListener("click", function () {
        const nextTheme =
            root.dataset.theme === "dark" ? "light" : "dark";

        applyTheme(nextTheme);

        try {
            localStorage.setItem("theme", nextTheme);
        } catch (error) {
            console.warn("Could not save theme preference.");
        }
    });

    systemTheme.addEventListener("change", function (event) {
        if (!hasUserPreference) {
            applyTheme(event.matches ? "dark" : "light");
        }
    });
})();
```

#### styles.css
```css
:root {
    --bg:#f7f8f5;
    --ink:#1d2422;
    --muted:#727b76;
    --line:#dfe4df;
    --green:#b9f279;
    --deep:#1e2926;
    --panel:#eef1ec;
    --serif:Georgia,"Times New Roman",serif;
    --sans:"DM Sans",Arial,sans-serif;
    --display:"Manrope",Arial,sans-serif;
    --mono:"DM Mono",monospace
}
* {
    box-sizing:border-box
}
html {
    scroll-behavior:smooth;
    scroll-padding-top:95px
}
body {
    margin:0;
    background:var(--bg);
    color:var(--ink);
    font-family:var(--sans);
    font-size:14px;
    line-height:1.7
}
a {
    color:inherit;
    text-decoration:none
}
button,input,textarea {
    font:inherit
}
.section-wrap {
    width:min(1160px,calc(100% - 72px));
    margin-inline:auto
}
.topline {
    height:31px;
    background:var(--deep);
    color:#cbd5cf;
    display:flex;
    justify-content:space-between;
    align-items:center;
    padding:0 max(36px,calc((100vw - 1160px)/2));
    font-family:var(--mono);
    font-size:8px;
    letter-spacing:.04em
}
.pulse {
    display:inline-block;
    width:6px;
    height:6px;
    border-radius:50%;
    background:var(--green);
    margin-right:7px;
    box-shadow:0 0 0 3px #b9f27920
}
.topline-right {
    color:#9da9a2
}
.topline-right b {
    padding:0 6px;
    color:var(--green)
}
.site-header {
    height:78px;
    display:flex;
    align-items:center;
    justify-content:space-between;
    padding:0 max(36px,calc((100vw - 1160px)/2));
    border-bottom:1px solid var(--line);
    position:sticky;
    top:0;
    background:rgba(247,248,245,.94);
    backdrop-filter:blur(14px);
    z-index:20
}
.brand {
    display:flex;
    align-items:center;
    gap:10px;
    font-family:var(--display);
    font-weight:800;
    font-size:13px;
    letter-spacing:-.04em
}
.brand-icon {
    display:grid;
    place-items:center;
    width:34px;
    height:34px;
    border-radius:7px;
    background:var(--deep);
    color:var(--green);
    font-family:var(--mono);
    font-size:12px
}
.brand-icon span {
    color:#fff
}

.brand-logo {
    display: block;
    width: 34px;
    height: 34px;
    object-fit: contain;
    border-radius: 7px;
}

.brand-muted {
    color:#818a84;
    font-weight:500
}
.nav {
    display:flex;
    align-items:center;
    gap:30px;
    font-size:11px;
    font-weight:600
}
.nav-link {
    color:#68716c;
    transition:color .2s
}
.nav-link:hover,.nav-link.active {
    color:var(--ink)
}
.nav-contact {
    background:var(--green);
    padding:11px 15px;
    border-radius:3px;
    color:var(--ink)
}
.nav-contact span {
    margin-left:10px
}
.menu-toggle {
    display:none;
    background:none;
    border:0
}
.hero {
    min-height:625px;
    padding-top:86px;
    padding-bottom:80px;
    display:grid;
    grid-template-columns:1.05fr .95fr;
    align-items:center;
    gap:40px;
    position:relative
}
.eyebrow {
    font-family:var(--mono);
    font-size:10px;
    letter-spacing:.08em;
    color:#7a847d;
    margin:0 0 25px
}
.terminal-mark {
    color:#568d35;
    font-weight:500;
    margin-right:8px
}
h1,h2,h3,p {
    margin-top:0
}
h1,h2 {
    font-family:var(--display);
    letter-spacing:-.075em;
    line-height:1.09;
    font-weight:650
}
h1 {
    font-size:clamp(43px,5.1vw,70px);
    margin-bottom:24px
}
h2 {
    font-size:clamp(40px,4.3vw,59px);
    margin-bottom:23px
}
.hero-accent {
    color:#648b51
}
.serif-accent {
    font-family:var(--serif);
    font-style:italic;
    font-weight:400;
    letter-spacing:-.07em
}
.hero-intro {
    max-width:500px;
    color:#69736d;
    font-size:15px;
    line-height:1.9
}
.hero-actions {
    display:flex;
    align-items:center;
    gap:26px;
    margin-top:29px
}
.button {
    display:inline-flex;
    justify-content:center;
    align-items:center;
    gap:24px;
    padding:14px 18px;
    border:1px solid var(--ink);
    font-size:11px;
    font-weight:700;
    transition:transform .2s,background .2s;
    cursor:pointer
}
.button:hover {
    transform:translateY(-2px)
}
.button-primary {
    background:var(--deep);
    color:#fff
}
.button-primary:hover {
    background:#33423b
}
.text-link {
    font-size:11px;
    font-weight:700
}
.text-link span {
    margin-left:9px
}
.hero-facts {
    display:flex;
    gap:36px;
    margin-top:55px
}
.hero-facts div {
    display:flex;
    flex-direction:column;
    gap:4px
}
.fact-label {
    font-family:var(--mono);
    font-size:8px;
    letter-spacing:.08em;
    color:#849087
}
.hero-facts strong {
    font-size:10px;
    font-weight:600
}
.terminal-wrap {
    height:410px;
    position:relative;
    display:grid;
    place-items:center
}
.terminal-window {
    position:relative;
    z-index:2;
    width:min(100%,430px);
    background:#202b27;
    color:#e5ece7;
    border:1px solid #36443d;
    border-radius:8px;
    box-shadow:0 28px 70px #23342a20;
    overflow:hidden;
    transform:rotate(1deg)
}
.terminal-titlebar {
    height:42px;
    background:#2a3731;
    border-bottom:1px solid #3b4941;
    display:flex;
    align-items:center;
    justify-content:space-between;
    padding:0 14px;
    font-family:var(--mono);
    font-size:9px;
    color:#aebbb2
}
.window-dots {
    display:flex;
    gap:5px
}
.window-dots i {
    width:7px;
    height:7px;
    border-radius:50%;
    background:#64766a
}
.window-dots i:first-child {
    background:#e58c7c
}
.window-dots i:nth-child(2) {
    background:#e7c56d
}
.window-dots i:nth-child(3) {
    background:#8acb78
}
.terminal-lock {
    font-size:7px;
    color:var(--green)
}
.terminal-body {
    padding:24px 24px 17px;
    min-height:275px;
    font-family:var(--mono);
    font-size:10px;
    line-height:1.9
}
.terminal-body p {
    margin:0 0 10px
}
.term-muted {
    color:#7c8b80
}
.term-green {
    color:#b9f279
}
.term-blue {
    color:#8fc7df
}
.term-output {
    padding-left:13px;
    color:#c5d1c8
}
.cursor {
    display:inline-block;
    width:7px;
    height:13px;
    background:var(--green);
    vertical-align:middle;
    animation:blink 1s steps(2,start) infinite
}
@keyframes blink {
    to {
        visibility:hidden
    }
}
.terminal-status {
    border-top:1px solid #39473f;
    display:flex;
    justify-content:space-between;
    padding:10px 15px;
    font-family:var(--mono);
    font-size:8px;
    color:#91a095
}
.terminal-status b {
    padding:0 4px;
    color:#5e6d62
}
.status-dot {
    display:inline-block;
    width:5px;
    height:5px;
    border-radius:50%;
    background:var(--green);
    margin-right:6px
}
.terminal-chip {
    position:absolute;
    z-index:3;
    background:#fff;
    border:1px solid var(--line);
    box-shadow:0 8px 24px #17261c10;
    padding:10px 13px;
    font-size:9px;
    font-weight:700;
    white-space:nowrap
}
.terminal-chip span {
    color:#558544;
    margin-right:7px
}
.chip-top {
    top:32px;
    right:-5px;
    transform:rotate(4deg)
}
.chip-bottom {
    bottom:29px;
    left:-15px;
    transform:rotate(-3deg)
}
.hero-grid-decoration {
    position:absolute;
    right:-7px;
    top:23px;
    width:130px;
    height:130px;
    opacity:.55;
    background-image:radial-gradient(#aebcaf 1px,transparent 1px);
    background-size:10px 10px
}
.scroll-cue {
    position:absolute;
    bottom:25px;
    left:0;
    display:flex;
    align-items:center;
    gap:12px;
    font-family:var(--mono);
    font-size:8px;
    letter-spacing:.08em;
    color:#78837b
}
.scroll-cue span {
    height:1px;
    width:38px;
    background:#9ca89e
}
.signal-strip {
    background:var(--green);
    padding:17px 0
}
.signal-inner {
    display:flex;
    justify-content:space-between;
    align-items:center;
    font-family:var(--mono);
    font-size:9px;
    letter-spacing:.12em;
    font-weight:500
}
.signal-inner b {
    font-size:13px;
    font-weight:400;
    color:#658e4e
}
.section {
    padding-top:105px;
    padding-bottom:110px
}
.section-heading {
    display:flex;
    justify-content:space-between;
    align-items:center;
    border-bottom:1px solid var(--line);
    padding-bottom:15px;
    margin-bottom:54px
}
.section-heading .eyebrow {
    margin:0
}
.section-number {
    font-family:var(--mono);
    font-size:8px;
    letter-spacing:.13em;
    color:#8d968f
}
.about-grid {
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:65px
}
.about-copy {
    max-width:500px
}
.lead {
    font-size:17px;
    line-height:1.7;
    letter-spacing:-.025em
}
.about-copy>p:not(.lead) {
    color:#707b73;
    font-size:12px;
    line-height:2
}
.underlined {
    display:inline-block;
    margin-top:14px;
    border-bottom:1px solid #b8c0b8;
    padding-bottom:7px
}
.principles {
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:30px;
    margin-top:76px
}
.principles article {
    border-top:1px solid var(--line);
    padding-top:17px
}
.principle-icon {
    font-family:var(--mono);
    font-size:11px;
    color:#6e9c57
}
.principles h3 {
    font-family:var(--display);
    font-size:13px;
    letter-spacing:-.035em;
    margin:13px 0 7px
}
.principles p {
    font-size:11px;
    color:#7a847d;
    max-width:260px
}
.stack-section {
    background:#edf1eb
}
.stack-section .section {
    padding-top:96px;
    padding-bottom:100px
}
.stack-heading,.projects-heading,.roadmap-heading {
    display:flex;
    justify-content:space-between;
    align-items:end;
    margin-bottom:37px
}
.stack-heading h2,.projects-heading h2,.roadmap-heading h2 {
    margin:0
}
.stack-heading>p,.projects-heading>p,.roadmap-heading>p {
    max-width:315px;
    font-size:12px;
    color:#727c74;
    line-height:1.9;
    margin:0 0 5px
}
.stack-grid {
    display:grid;
    grid-template-columns:repeat(4,1fr);
    gap:13px
}
.stack-card {
    background:#f8f9f6;
    border:1px solid #dce4db;
    padding:20px 17px 17px;
    min-height:245px;
    display:flex;
    flex-direction:column
}
.stack-card-top {
    display:flex;
    align-items:center;
    justify-content:space-between;
    margin-bottom:24px
}
.stack-icon {
    display:grid;
    place-items:center;
    width:34px;
    height:34px;
    background:#e7f6d8;
    color:#4e7c3d;
    border-radius:5px;
    font-family:var(--mono);
    font-size:14px
}
.stack-index {
    font-family:var(--mono);
    font-size:8px;
    color:#9ba49b
}
.stack-card h3 {
    font-family:var(--display);
    font-size:14px;
    letter-spacing:-.04em;
    margin-bottom:13px
}
.tag-list {
    display:flex;
    flex-wrap:wrap;
    gap:5px
}
.tag-list span {
    background:#edf0ea;
    padding:4px 7px;
    font-size:9px;
    color:#4e5c51
}
.stack-card>p {
    font-size:10px;
    color:#788179;
    line-height:1.8;
    margin:15px 0 17px
}
.stack-status {
    margin-top:auto;
    font-family:var(--mono);
    font-size:7px;
    letter-spacing:.06em;
    align-self:flex-start;
    padding:5px 7px
}
.status-practicing {
    background:#e5f5d7;
    color:#4f783b
}
.status-roadmap {
    background:#f4ecd0;
    color:#8a7331
}
.stack-note {
    margin:18px 0 0;
    color:#7c857d;
    font-size:9px
}
.stack-note span {
    display:inline-grid;
    place-items:center;
    border:1px solid #b7c3b4;
    border-radius:50%;
    width:15px;
    height:15px;
    font-family:var(--mono);
    margin-right:5px
}
.project-filters {
    display:flex;
    gap:22px;
    border-bottom:1px solid var(--line);
    margin-bottom:26px
}
.filter-button {
    background:none;
    border:0;
    padding:0 0 13px;
    font-size:10px;
    color:#879087;
    cursor:pointer
}
.filter-button.active {
    color:var(--ink);
    border-bottom:2px solid #5d8b4a;
    font-weight:700
}
.filter-button span {
    font-size:8px;
    margin-left:6px
}
.project-grid {
    display:grid;
    grid-template-columns:repeat(2,1fr);
    gap:42px 25px
}
.project-card[hidden] {
    display:none
}
.project-art {
    height:245px;
    position:relative;
    overflow:hidden;
    display:flex;
    align-items:center;
    justify-content:center
}
.art-label {
    position:absolute;
    left:15px;
    bottom:12px;
    font-family:var(--mono);
    font-size:7px;
    letter-spacing:.1em;
    color:#738077
}
.art-proxmox {
    background:#e4eae1;
    flex-direction:column
}
.diagram-node {
    position:relative;
    z-index:1;
    display:flex;
    flex-direction:column;
    align-items:center;
    justify-content:center;
    gap:3px;
    background:#f8faf6;
    border:1px solid #c8d4c7;
    width:132px;
    height:64px;
    border-radius:5px;
    box-shadow:0 7px 20px #283e2910
}
.diagram-node>span {
    font-size:12px;
    color:#5c8b4c
}
.diagram-node b {
    font-family:var(--mono);
    font-size:9px
}
.diagram-node small {
    font-size:8px;
    color:#859087
}
.diagram-connector {
    height:27px;
    width:1px;
    background:#8ba384
}
.diagram-vms {
    display:flex;
    gap:12px
}
.diagram-vms .diagram-node {
    width:120px;
    height:58px
}
.art-nginx {
    background:#dce8e1;
    gap:24px
}
.browser-frame {
    width:58%;
    height:165px;
    background:#f9faf6;
    border:1px solid #ccd8ce;
    border-radius:5px;
    box-shadow:0 15px 28px #1d362319;
    transform:rotate(-3deg);
    overflow:hidden
}
.browser-bar {
    height:24px;
    background:#e9eee7;
    border-bottom:1px solid #dce4db;
    display:flex;
    align-items:center;
    gap:4px;
    padding:0 8px
}
.browser-bar i,.code-title i {
    width:5px;
    height:5px;
    border-radius:50%;
    background:#a2b0a0
}
.browser-bar span {
    font-family:var(--mono);
    font-size:7px;
    color:#839087;
    margin-left:7px
}
.browser-content {
    padding:17px
}
.browser-kicker {
    font-family:var(--mono);
    font-size:6px;
    color:#719363;
    display:block;
    margin-bottom:7px
}
.browser-content>b {
    font-family:var(--display);
    font-size:15px;
    letter-spacing:-.05em;
    line-height:1.2;
    display:block
}
.browser-lines {
    margin-top:11px;
    display:grid;
    gap:4px
}
.browser-lines i {
    height:3px;
    background:#e1e7df;
    width:85%
}
.browser-lines i:nth-child(2) {
    width:68%
}
.browser-lines i:nth-child(3) {
    width:76%
}
.browser-badge {
    display:inline-block;
    margin-top:10px;
    background:#e4f5d9;
    color:#5e854d;
    font-family:var(--mono);
    font-size:6px;
    padding:4px
}
.web-stack {
    display:flex;
    flex-direction:column;
    align-items:center;
    gap:4px;
    font-family:var(--mono);
    font-size:7px;
    color:#536b59
}
.web-stack span {
    background:#f7faf5;
    border:1px solid #cbd9cb;
    padding:7px 9px;
    white-space:nowrap
}
.web-stack b {
    font-weight:400;
    color:#7c9c70
}
.art-spotiflac {
    background:#e5e3f1
}
.code-window {
    width:75%;
    background:#292d38;
    border:1px solid #414657;
    border-radius:5px;
    box-shadow:0 15px 30px #2725381c;
    transform:rotate(2deg);
    overflow:hidden
}
.code-title {
    height:27px;
    background:#343846;
    display:flex;
    align-items:center;
    gap:4px;
    padding:0 10px
}
.code-title i:first-child {
    background:#e58c7c
}
.code-title i:nth-child(2) {
    background:#e7c56d
}
.code-title i:nth-child(3) {
    background:#8acb78
}
.code-title span {
    font-family:var(--mono);
    font-size:7px;
    color:#abb1c0;
    margin-left:8px
}
.code-lines {
    padding:13px 15px 17px;
    font-family:var(--mono);
    font-size:8px;
    line-height:2;
    color:#d9d9e5
}
.code-lines p {
    margin:0
}
.code-lines em {
    color:#c5a9f1;
    font-style:normal
}
.code-lines strong {
    color:#9bd7c0
}
.code-lines b {
    color:#f2d18a;
    font-weight:400
}
.code-lines .code-comment {
    color:#8b95a7;
    margin-top:7px
}
.code-stamp {
    position:absolute;
    right:20px;
    bottom:33px;
    width:47px;
    height:47px;
    background:#b6a9e8;
    border-radius:50%;
    display:grid;
    place-content:center;
    text-align:center;
    font-family:var(--mono);
    font-size:11px;
    line-height:1.1;
    color:#312d49;
    transform:rotate(10deg)
}
.project-info {
    display:flex;
    justify-content:space-between;
    align-items:start;
    padding-top:17px
}
.project-type {
    font-family:var(--mono);
    font-size:7px;
    letter-spacing:.05em;
    color:#7e8980;
    margin-bottom:6px
}
.project-info h3 {
    font-family:var(--display);
    font-size:17px;
    letter-spacing:-.05em;
    margin:0
}
.project-year {
    font-family:var(--mono);
    font-size:9px;
    color:#849087
}
.project-description {
    font-size:11px;
    color:#727c74;
    line-height:1.9;
    margin:13px 0
}
.project-outcomes {
    display:flex;
    flex-wrap:wrap;
    gap:6px
}
.project-outcomes span {
    border:1px solid var(--line);
    padding:5px 7px;
    font-size:8px;
    color:#657168
}
.project-link {
    display:inline-flex;
    gap:14px;
    align-items:center;
    border-bottom:1px solid #bdc6bd;
    padding-bottom:5px;
    margin-top:17px;
    font-size:10px;
    font-weight:700
}
.project-link span {
    color:#578648
}
.portfolio-note {
    font-size:9px;
    color:#8a938b;
    margin-top:30px
}
.roadmap-section {
    background:#202b27;
    color:#f0f4ef
}
.roadmap-section .section {
    padding-top:95px;
    padding-bottom:100px
}
.roadmap-section .section-heading {
    border-color:#3c4840
}
.roadmap-section .eyebrow,.roadmap-section .section-number {
    color:#a4b1a6
}
.roadmap-heading>p {
    color:#aab5ac
}
.roadmap-list {
    border-top:1px solid #3c4840
}
.roadmap-list article {
    display:grid;
    grid-template-columns:55px 1fr 30px;
    gap:20px;
    padding:22px 0;
    border-bottom:1px solid #3c4840;
    align-items:start
}
.roadmap-number {
    font-family:var(--mono);
    font-size:10px;
    color:var(--green);
    padding-top:4px
}
.roadmap-state {
    font-family:var(--mono);
    font-size:7px;
    letter-spacing:.12em;
    color:#a8b5a9
}
.roadmap-list h3 {
    font-family:var(--display);
    font-size:17px;
    letter-spacing:-.04em;
    margin:4px 0 5px
}
.roadmap-list p {
    font-size:11px;
    color:#aab5ac;
    margin:0;
    max-width:650px
}
.roadmap-check {
    color:var(--green);
    font-size:14px
}
.roadmap-pending {
    color:#6b786d
}
.contact-section .section {
    padding-top:100px;
    padding-bottom:100px
}
.contact-grid {
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:80px
}
.contact-intro {
    font-size:12px;
    color:#727c74;
    max-width:380px;
    line-height:1.9;
    margin-bottom:25px
}
.email-link {
    display:inline-block;
    font-family:var(--mono);
    font-size:12px;
    font-weight:500;
    border-bottom:1px solid #aeb8ae;
    padding-bottom:7px
}
.email-link span {
    margin-left:10px
}
.social-links {
    display:flex;
    gap:20px;
    margin-top:24px;
    font-size:10px;
    font-weight:700
}
.contact-form {
    display:flex;
    flex-direction:column;
    align-items:stretch
}
.contact-form label {
    font-family:var(--mono);
    font-size:8px;
    letter-spacing:.08em;
    color:#707b72;
    margin-bottom:7px
}
.contact-form input,.contact-form textarea {
    background:transparent;
    border:0;
    border-bottom:1px solid #d5ddd4;
    border-radius:0;
    padding:10px 0 13px;
    margin-bottom:23px;
    outline:none;
    color:var(--ink);
    resize:vertical
}
.contact-form input:focus,.contact-form textarea:focus {
    border-color:#76a25e
}
.contact-form input::placeholder,.contact-form textarea::placeholder {
    color:#a3aca4;
    font-size:11px
}
.contact-form .button {
    align-self:flex-start
}
.form-note {
    font-size:9px;
    color:#879087;
    line-height:1.6;
    margin:11px 0 0
}
.footer {
    background:#edf1eb;
    border-top:1px solid var(--line);
    padding:25px 0
}
.footer-inner {
    display:flex;
    align-items:center;
    gap:25px;
    flex-wrap:wrap
}
.footer-inner>p {
    font-size:9px;
    color:#78837a;
    margin:0
}
.footer-links {
    display:flex;
    gap:17px;
    margin-left:auto;
    font-size:9px;
    font-weight:700
}
.copyright {
    font-family:var(--mono);
    font-size:7px;
    letter-spacing:.1em;
    color:#8a958b
}
@media(max-width:900px) {
    .site-header {
        padding-inline:25px
    }
    .topline {
        padding-inline:25px
    }
    .section-wrap {
        width:calc(100% - 50px)
    }
    .nav {
        gap:17px
    }
    .hero {
        gap:20px
    }
    .terminal-chip {
        font-size:8px
    }
    .stack-grid {
        grid-template-columns:repeat(2,1fr)
    }
    .contact-grid {
        gap:45px
    }
}
@media(max-width:650px) {
    html {
        scroll-padding-top:75px
    }
    .topline {
        padding-inline:16px;
        font-size:7px
    }
    .topline-right {
        display:none
    }
    .site-header {
        height:70px;
        padding-inline:20px
    }
    .section-wrap {
        width:calc(100% - 40px)
    }
    .menu-toggle {
        display:flex;
        width:40px;
        height:40px;
        flex-direction:column;
        gap:6px;
        align-items:center;
        justify-content:center;
        cursor:pointer
    }
    .menu-toggle span {
        height:1px;
        width:22px;
        background:var(--ink)
    }
    .nav {
        display:none;
        position:absolute;
        top:69px;
        left:0;
        right:0;
        background:var(--bg);
        padding:20px;
        flex-direction:column;
        align-items:stretch;
        gap:0;
        border-bottom:1px solid var(--line)
    }
    .nav.open {
        display:flex
    }
    .nav-link {
        padding:12px 0;
        border-bottom:1px solid var(--line)
    }
    .nav-contact {
        margin-top:12px;
        padding:12px 15px;
        border:0
    }
    .hero {
        display:flex;
        flex-direction:column;
        align-items:stretch;
        padding-top:59px;
        padding-bottom:84px;
        gap:0
    }
    .hero h1 {
        font-size:clamp(40px,11vw,58px)
    }
    .hero-intro {
        font-size:13px
    }
    .hero-facts {
        gap:18px;
        margin-top:37px;
        flex-wrap:wrap
    }
    .hero-facts strong {
        font-size:9px
    }
    .terminal-wrap {
        height:350px;
        margin-top:26px
    }
    .terminal-window {
        width:100%
    }
    .terminal-body {
        min-height:245px;
        padding:20px;
        font-size:9px
    }
    .chip-top {
        right:-3px;
        top:5px
    }
    .chip-bottom {
        left:-3px;
        bottom:7px
    }
    .hero-grid-decoration {
        right:0
    }
    .scroll-cue {
        bottom:20px
    }
    .signal-inner {
        gap:8px;
        font-size:7px;
        letter-spacing:.04em
    }
    .signal-inner b {
        font-size:10px
    }
    .section {
        padding-top:75px;
        padding-bottom:80px
    }
    .section-heading {
        margin-bottom:36px
    }
    .about-grid {
        grid-template-columns:1fr;
        gap:20px
    }
    .about-grid h2,.stack-heading h2,.projects-heading h2,.roadmap-heading h2,.contact-grid h2 {
        font-size:45px
    }
    .lead {
        font-size:16px
    }
    .principles {
        grid-template-columns:1fr;
        gap:18px;
        margin-top:45px
    }
    .principles article {
        display:grid;
        grid-template-columns:35px 1fr;
        column-gap:10px;
        padding-top:14px
    }
    .principle-icon {
        grid-row:span 2
    }
    .principles h3 {
        margin:0 0 4px
    }
    .principles p {
        margin:0;
        max-width:none
    }
    .stack-section .section,.roadmap-section .section,.contact-section .section {
        padding-block:75px
    }
    .stack-heading,.projects-heading,.roadmap-heading {
        display:block
    }
    .stack-heading>p,.projects-heading>p,.roadmap-heading>p {
        margin-top:18px
    }
    .stack-grid {
        grid-template-columns:1fr;
        gap:10px
    }
    .stack-card {
        min-height:0;
        padding:18px
    }
    .stack-card-top {
        margin-bottom:15px
    }
    .stack-card>p {
        margin-bottom:14px
    }
    .project-filters {
        gap:15px;
        overflow-x:auto
    }
    .filter-button {
        white-space:nowrap;
        font-size:9px
    }
    .project-grid {
        grid-template-columns:1fr;
        gap:34px
    }
    .project-art {
        height:225px
    }
    .roadmap-list article {
        grid-template-columns:28px 1fr 18px;
        gap:12px;
        padding:19px 0
    }
    .roadmap-list h3 {
        font-size:15px
    }
    .roadmap-list p {
        font-size:10px
    }
    .contact-grid {
        grid-template-columns:1fr;
        gap:42px
    }
    .footer-inner {
        gap:15px
    }
    .footer-inner>p {
        order:3;
        width:100%
    }
    .footer-links {
        margin-left:auto;
        gap:12px
    }
    .copyright {
        width:100%
    }
}

/* Theme toggle button */
:root {
    color-scheme: light;
}

.theme-toggle {
    display: inline-grid;
    place-items: center;
    flex-shrink: 0;
    width: 38px;
    height: 38px;
    padding: 0;
    border: 1px solid var(--line);
    border-radius: 5px;
    background: transparent;
    color: var(--ink);
    cursor: pointer;
    transition: background .2s, border-color .2s;
}

.theme-toggle:hover {
    background: var(--panel);
    border-color: var(--muted);
}

.theme-toggle:focus-visible {
    outline: 2px solid var(--ink);
    outline-offset: 4px;
}

.theme-icon {
    width: 18px;
    height: 18px;
}

.theme-icon-sun {
    display: none;
}

html[data-theme="dark"] {
    color-scheme: dark;

    --bg: #111714;
    --ink: #e6ede7;
    --muted: #a0ada3;
    --line: #303d34;
    --green: #b9f279;
    --deep: #1e2926;
    --panel: #19221c;

    --surface: #202c24;
    --subtle: #87978b;
    --accent: #a4d780;
    --on-accent: #182211;
    --border-strong: #475b4b;
}

html[data-theme="dark"] .theme-icon-moon {
    display: none;
}

html[data-theme="dark"] .theme-icon-sun {
    display: block;
}

/* Header */
html[data-theme="dark"] .topline {
    background: #0c120f;
    color: #cbd5cf;
}

html[data-theme="dark"] .topline-right {
    color: var(--muted);
}

html[data-theme="dark"] .site-header {
    background: rgba(17, 23, 20, .94);
}

html[data-theme="dark"] .brand-icon {
    background: #26362b;
}

html[data-theme="dark"] .brand-muted,
html[data-theme="dark"] .nav-link {
    color: var(--muted);
}

html[data-theme="dark"] .nav-link:hover,
html[data-theme="dark"] .nav-link.active {
    color: var(--ink);
}

html[data-theme="dark"] .nav-contact,
html[data-theme="dark"] .nav-contact:hover,
html[data-theme="dark"] .nav-contact.active {
    background: var(--green);
    color: var(--on-accent);
}

html[data-theme="dark"] .menu-toggle {
    color: var(--ink);
}

/* Typography and hero */
html[data-theme="dark"] .eyebrow,
html[data-theme="dark"] .fact-label,
html[data-theme="dark"] .section-number,
html[data-theme="dark"] .scroll-cue {
    color: var(--subtle);
}

html[data-theme="dark"] .terminal-mark,
html[data-theme="dark"] .hero-accent,
html[data-theme="dark"] .principle-icon {
    color: var(--accent);
}

html[data-theme="dark"] .hero-intro,
html[data-theme="dark"] .about-copy > p:not(.lead),
html[data-theme="dark"] .principles p,
html[data-theme="dark"] .stack-heading > p,
html[data-theme="dark"] .projects-heading > p,
html[data-theme="dark"] .roadmap-heading > p,
html[data-theme="dark"] .contact-intro {
    color: var(--muted);
}

html[data-theme="dark"] .button {
    border-color: var(--border-strong);
}

html[data-theme="dark"] .button-primary {
    background: var(--green);
    border-color: var(--green);
    color: var(--on-accent);
}

html[data-theme="dark"] .button-primary:hover {
    background: #c9f79b;
    border-color: #c9f79b;
}

html[data-theme="dark"] .underlined,
html[data-theme="dark"] .project-link,
html[data-theme="dark"] .email-link {
    border-color: var(--border-strong);
}

html[data-theme="dark"] .scroll-cue span {
    background: var(--border-strong);
}

html[data-theme="dark"] .hero-grid-decoration {
    opacity: .35;
    background-image: radial-gradient(#65816a 1px, transparent 1px);
}

/* Terminal */
html[data-theme="dark"] .terminal-window {
    background: #17211b;
    border-color: #354a3c;
    color: #e5ece7;
    box-shadow: 0 28px 70px #00000055;
}

html[data-theme="dark"] .terminal-titlebar {
    background: #223127;
    border-bottom-color: #354a3c;
    color: #b4c3b8;
}

html[data-theme="dark"] .term-muted {
    color: #9aafa0;
}

html[data-theme="dark"] .term-output {
    color: #c5d1c8;
}

html[data-theme="dark"] .terminal-status {
    border-top-color: #354a3c;
    color: #a1b3a6;
}

html[data-theme="dark"] .terminal-status b {
    color: #809586;
}

html[data-theme="dark"] .terminal-chip {
    background: var(--surface);
    border-color: var(--border-strong);
    color: var(--ink);
    box-shadow: 0 8px 24px #00000040;
}

html[data-theme="dark"] .terminal-chip span {
    color: var(--green);
}

/* Signal strip */
html[data-theme="dark"] .signal-strip {
    background: var(--green);
    color: var(--on-accent);
}

html[data-theme="dark"] .signal-inner b {
    color: #456630;
}

/* Stack section */
html[data-theme="dark"] .stack-section {
    background: var(--panel);
}

html[data-theme="dark"] .stack-card {
    background: var(--bg);
    border-color: var(--line);
}

html[data-theme="dark"] .stack-icon {
    background: #2b4025;
    color: var(--green);
}

html[data-theme="dark"] .stack-index,
html[data-theme="dark"] .stack-note {
    color: var(--subtle);
}

html[data-theme="dark"] .tag-list span {
    background: #26342b;
    color: #c4d3c7;
}

html[data-theme="dark"] .stack-card > p {
    color: var(--muted);
}

html[data-theme="dark"] .status-practicing {
    background: #2b4025;
    color: #b9e596;
}

html[data-theme="dark"] .status-roadmap {
    background: #3c3420;
    color: #e2c879;
}

html[data-theme="dark"] .stack-note span {
    border-color: var(--border-strong);
}

/* Projects */
html[data-theme="dark"] .filter-button {
    color: var(--muted);
}

html[data-theme="dark"] .filter-button.active {
    color: var(--ink);
    border-bottom-color: var(--green);
}

html[data-theme="dark"] .art-label,
html[data-theme="dark"] .project-type,
html[data-theme="dark"] .project-year,
html[data-theme="dark"] .portfolio-note {
    color: var(--subtle);
}

html[data-theme="dark"] .project-description {
    color: var(--muted);
}

html[data-theme="dark"] .project-outcomes span {
    border-color: var(--line);
    color: #b2c3b6;
}

html[data-theme="dark"] .project-link span {
    color: var(--green);
}

/* Proxmox illustration */
html[data-theme="dark"] .art-proxmox {
    background: #202f24;
}

html[data-theme="dark"] .diagram-node {
    background: #17221b;
    border-color: #425c46;
    box-shadow: 0 7px 20px #00000030;
}

html[data-theme="dark"] .diagram-node > span {
    color: var(--green);
}

html[data-theme="dark"] .diagram-node small {
    color: var(--muted);
}

html[data-theme="dark"] .diagram-connector {
    background: #688a62;
}

/* Nginx illustration */
html[data-theme="dark"] .art-nginx {
    background: #1e3029;
}

html[data-theme="dark"] .browser-frame {
    background: #142019;
    border-color: #40594a;
    box-shadow: 0 15px 28px #00000040;
}

html[data-theme="dark"] .browser-bar {
    background: #27382c;
    border-bottom-color: #40513f;
}

html[data-theme="dark"] .browser-bar i {
    background: #809b80;
}

html[data-theme="dark"] .browser-bar span {
    color: #afc0b2;
}

html[data-theme="dark"] .browser-kicker {
    color: var(--accent);
}

html[data-theme="dark"] .browser-lines i {
    background: #344a39;
}

html[data-theme="dark"] .browser-badge {
    background: #2b4025;
    color: #b9e596;
}

html[data-theme="dark"] .web-stack {
    color: #b3cbb9;
}

html[data-theme="dark"] .web-stack span {
    background: #19281f;
    border-color: #425c46;
}

html[data-theme="dark"] .web-stack b {
    color: var(--accent);
}

/* Code illustration */
html[data-theme="dark"] .art-spotiflac {
    background: #282537;
}

html[data-theme="dark"] .code-window {
    background: #1b1e29;
    border-color: #45475f;
    box-shadow: 0 15px 30px #00000045;
}

html[data-theme="dark"] .code-title {
    background: #2d3040;
}

/* Roadmap */
html[data-theme="dark"] .roadmap-section {
    background: #17211c;
    color: var(--ink);
}

html[data-theme="dark"] .roadmap-section .section-heading,
html[data-theme="dark"] .roadmap-list,
html[data-theme="dark"] .roadmap-list article {
    border-color: #35483a;
}

html[data-theme="dark"] .roadmap-section .eyebrow,
html[data-theme="dark"] .roadmap-section .section-number,
html[data-theme="dark"] .roadmap-heading > p,
html[data-theme="dark"] .roadmap-state,
html[data-theme="dark"] .roadmap-list p {
    color: #aabcae;
}

html[data-theme="dark"] .roadmap-pending {
    color: #8ca18f;
}

/* Contact form */
html[data-theme="dark"] .contact-form label {
    color: var(--muted);
}

html[data-theme="dark"] .contact-form input,
html[data-theme="dark"] .contact-form textarea {
    background: transparent;
    border-bottom-color: var(--border-strong);
    color: var(--ink);
}

html[data-theme="dark"] .contact-form input:focus,
html[data-theme="dark"] .contact-form textarea:focus {
    border-color: var(--green);
}

html[data-theme="dark"] .contact-form input::placeholder,
html[data-theme="dark"] .contact-form textarea::placeholder {
    color: var(--subtle);
}

html[data-theme="dark"] .form-note {
    color: var(--muted);
}

/* Footer */
html[data-theme="dark"] .footer {
    background: var(--panel);
    border-top-color: var(--line);
}

html[data-theme="dark"] .footer-inner > p,
html[data-theme="dark"] .copyright {
    color: var(--muted);
}

/* Selection and focus */
html[data-theme="dark"] ::selection {
    background: var(--green);
    color: var(--on-accent);
}

html[data-theme="dark"] a:focus-visible,
html[data-theme="dark"] button:focus-visible,
html[data-theme="dark"] input:focus-visible,
html[data-theme="dark"] textarea:focus-visible {
    outline: 2px solid var(--green);
    outline-offset: 4px;
}


@media(prefers-reduced-motion:reduce) {
    html {
        scroll-behavior:auto
    }
    *,*::before,*::after {
        transition:none!important;
        animation:none!important
    }
}
```










