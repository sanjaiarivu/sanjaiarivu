<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Sanjai Arivalagan</title>
<link rel="preconnect" href="https://fonts.googleapis.com"/>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;1,9..40,300&family=Syne:wght@400;700;800&display=swap" rel="stylesheet"/>
<style>
/* ─── RESET ─── */
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0;}
html{scroll-behavior:smooth;}
body{
  background:#080808;
  color:#e8e2d9;
  font-family:'DM Sans',sans-serif;
  font-weight:300;
  overflow-x:hidden;
  cursor:none;
}

/* ─── CUSTOM CURSOR ─── */
#cur{
  position:fixed;width:10px;height:10px;
  background:#e8e2d9;border-radius:50%;
  pointer-events:none;z-index:9999;
  transform:translate(-50%,-50%);
  transition:transform .08s,width .3s,height .3s,background .3s;
  mix-blend-mode:difference;
}
#cur-ring{
  position:fixed;width:36px;height:36px;
  border:1px solid rgba(232,226,217,.4);border-radius:50%;
  pointer-events:none;z-index:9998;
  transform:translate(-50%,-50%);
  transition:transform .18s ease,width .3s,height .3s,opacity .3s;
}
body:has(a:hover) #cur{width:20px;height:20px;}
body:has(a:hover) #cur-ring{width:60px;height:60px;opacity:.5;}

/* ─── NOISE OVERLAY ─── */
body::before{
  content:'';position:fixed;inset:0;z-index:1000;
  background-image:url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='1'/%3E%3C/svg%3E");
  opacity:.028;pointer-events:none;
}

/* ─── CANVAS ─── */
#bgCanvas{position:fixed;inset:0;z-index:0;opacity:.35;}

/* ─── PAGE WRAPPER ─── */
.page{position:relative;z-index:2;}

/* ─────────────────────────────────────────
   HERO
───────────────────────────────────────── */
.hero{
  min-height:100vh;
  display:grid;
  grid-template-rows:auto 1fr auto;
  padding:0 48px;
  position:relative;overflow:hidden;
}

/* top nav bar */
.nav{
  display:flex;justify-content:space-between;align-items:center;
  padding:32px 0 0;
  font-family:'Syne',sans-serif;
  font-size:.7rem;letter-spacing:.2em;text-transform:uppercase;
  color:rgba(232,226,217,.45);
}
.nav-links{display:flex;gap:32px;}
.nav a{color:inherit;text-decoration:none;transition:color .3s;}
.nav a:hover{color:#e8e2d9;}
.status-dot{
  width:7px;height:7px;border-radius:50%;
  background:#4ade80;display:inline-block;
  margin-right:8px;
  box-shadow:0 0 10px #4ade80;
  animation:dotPulse 2s ease-in-out infinite;
}
@keyframes dotPulse{0%,100%{opacity:1;}50%{opacity:.4;}}

/* big name */
.hero-center{
  display:flex;flex-direction:column;
  justify-content:center;align-items:flex-start;
  padding:60px 0;
}
.hero-eyebrow{
  font-family:'Syne',sans-serif;
  font-size:.72rem;letter-spacing:.35em;text-transform:uppercase;
  color:rgba(232,226,217,.4);
  margin-bottom:24px;
  display:flex;align-items:center;gap:12px;
}
.hero-eyebrow::before{content:'';width:40px;height:1px;background:rgba(232,226,217,.25);}

.hero-name{
  font-family:'Bebas Neue',sans-serif;
  font-size:clamp(80px,13vw,180px);
  line-height:.9;
  letter-spacing:-.01em;
  color:#e8e2d9;
  overflow:hidden;
}
.hero-name .line{
  display:block;overflow:hidden;
}
.hero-name .line span{
  display:block;
  transform:translateY(110%);
  animation:slideUp .9s cubic-bezier(.16,1,.3,1) both;
}
.hero-name .line:nth-child(1) span{animation-delay:.1s;}
.hero-name .line:nth-child(2) span{animation-delay:.22s;}
@keyframes slideUp{to{transform:translateY(0);}}

.hero-sub{
  display:flex;align-items:center;gap:48px;
  margin-top:36px;
}
.hero-role-pill{
  background:rgba(232,226,217,.07);
  border:1px solid rgba(232,226,217,.12);
  border-radius:100px;
  padding:10px 22px;
  font-size:.82rem;letter-spacing:.06em;
  backdrop-filter:blur(8px);
  white-space:nowrap;
}
.hero-desc{
  max-width:340px;
  font-size:.92rem;line-height:1.7;
  color:rgba(232,226,217,.5);
}

/* hero bottom bar */
.hero-bottom{
  display:flex;justify-content:space-between;align-items:flex-end;
  padding-bottom:40px;
  font-family:'Syne',sans-serif;
  font-size:.68rem;letter-spacing:.15em;text-transform:uppercase;
}
.scroll-hint{
  display:flex;align-items:center;gap:10px;
  color:rgba(232,226,217,.3);
}
.scroll-line{
  width:48px;height:1px;
  background:rgba(232,226,217,.2);
  position:relative;overflow:hidden;
}
.scroll-line::after{
  content:'';position:absolute;inset:0;
  background:#e8e2d9;
  animation:scanLine 2s ease-in-out infinite;
}
@keyframes scanLine{0%{transform:translateX(-100%);}100%{transform:translateX(100%);}}

.location-tag{color:rgba(232,226,217,.3);}

/* big background letter */
.hero-bg-letter{
  position:absolute;right:-2vw;top:50%;transform:translateY(-50%);
  font-family:'Bebas Neue',sans-serif;
  font-size:40vw;line-height:1;
  color:rgba(232,226,217,.018);
  pointer-events:none;user-select:none;
  letter-spacing:-.05em;
}

/* ─────────────────────────────────────────
   MARQUEE DIVIDER
───────────────────────────────────────── */
.marquee-wrap{
  overflow:hidden;
  border-top:1px solid rgba(232,226,217,.08);
  border-bottom:1px solid rgba(232,226,217,.08);
  padding:18px 0;
  background:rgba(232,226,217,.02);
}
.marquee-track{
  display:flex;gap:0;
  animation:marqueeRun 20s linear infinite;
  white-space:nowrap;
}
.marquee-track span{
  font-family:'Bebas Neue',sans-serif;
  font-size:1.1rem;letter-spacing:.2em;
  color:rgba(232,226,217,.25);
  padding:0 40px;
}
.marquee-track span.accent{color:rgba(232,226,217,.07);}
@keyframes marqueeRun{to{transform:translateX(-50%);}}

/* ─────────────────────────────────────────
   ABOUT
───────────────────────────────────────── */
.about{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:0;
  padding:120px 48px;
  border-bottom:1px solid rgba(232,226,217,.08);
}
.about-left{padding-right:80px;}
.section-num{
  font-family:'Syne',sans-serif;
  font-size:.65rem;letter-spacing:.3em;
  color:rgba(232,226,217,.25);
  margin-bottom:48px;
}
.big-heading{
  font-family:'Bebas Neue',sans-serif;
  font-size:clamp(52px,7vw,96px);
  line-height:.92;
  letter-spacing:.01em;
}
.big-heading em{
  font-style:normal;
  -webkit-text-stroke:1px rgba(232,226,217,.4);
  color:transparent;
}
.about-right{
  display:flex;flex-direction:column;justify-content:flex-end;
  padding-left:40px;
  border-left:1px solid rgba(232,226,217,.08);
}
.about-text{
  font-size:1.05rem;line-height:1.8;
  color:rgba(232,226,217,.6);
  margin-bottom:40px;
}
.about-text strong{color:#e8e2d9;font-weight:400;}

.yaml-block{
  background:rgba(232,226,217,.03);
  border:1px solid rgba(232,226,217,.08);
  border-radius:4px;
  padding:28px 32px;
  font-family:'DM Sans',sans-serif;
  font-size:.85rem;line-height:2;
}
.yaml-block .k{color:rgba(232,226,217,.4);}
.yaml-block .v{color:#e8e2d9;}
.yaml-block .s{color:#86efac;}
.yaml-block .c{color:rgba(232,226,217,.2);font-style:italic;}

/* ─────────────────────────────────────────
   SKILLS
───────────────────────────────────────── */
.skills{
  padding:120px 48px;
  border-bottom:1px solid rgba(232,226,217,.08);
}
.skills-header{
  display:flex;justify-content:space-between;align-items:flex-end;
  margin-bottom:72px;
}
.skills-grid{
  display:grid;
  grid-template-columns:repeat(4,1fr);
  gap:1px;
  background:rgba(232,226,217,.08);
  border:1px solid rgba(232,226,217,.08);
}
.skill-cell{
  background:#080808;
  padding:36px 28px;
  transition:background .35s;
  position:relative;overflow:hidden;
}
.skill-cell::after{
  content:'';
  position:absolute;inset:0;
  background:rgba(232,226,217,.04);
  transform:scaleY(0);transform-origin:bottom;
  transition:transform .4s cubic-bezier(.16,1,.3,1);
}
.skill-cell:hover{background:#0f0f0f;}
.skill-cell:hover::after{transform:scaleY(1);}

.skill-cell-label{
  font-family:'Syne',sans-serif;
  font-size:.6rem;letter-spacing:.25em;text-transform:uppercase;
  color:rgba(232,226,217,.3);
  margin-bottom:20px;
}
.skill-items{display:flex;flex-direction:column;gap:10px;}
.skill-item{
  display:flex;align-items:center;justify-content:space-between;
  font-size:.88rem;color:rgba(232,226,217,.75);
  padding-bottom:10px;
  border-bottom:1px solid rgba(232,226,217,.05);
}
.skill-item:last-child{border-bottom:none;padding-bottom:0;}
.skill-bar-mini{
  width:50px;height:2px;background:rgba(232,226,217,.1);border-radius:2px;overflow:hidden;
}
.skill-bar-fill{
  height:100%;background:#e8e2d9;border-radius:2px;
  transform:scaleX(0);transform-origin:left;
  transition:transform 1s cubic-bezier(.16,1,.3,1);
}
.skill-cell:hover .skill-bar-fill{transform:scaleX(1);}

/* ─────────────────────────────────────────
   EXPERIENCE
───────────────────────────────────────── */
.experience{
  padding:120px 48px;
  border-bottom:1px solid rgba(232,226,217,.08);
}
.exp-list{margin-top:72px;}
.exp-item{
  display:grid;
  grid-template-columns:180px 1fr auto;
  align-items:start;
  gap:40px;
  padding:40px 0;
  border-top:1px solid rgba(232,226,217,.08);
  transition:padding-left .4s cubic-bezier(.16,1,.3,1);
  cursor:default;
}
.exp-item:hover{padding-left:24px;}
.exp-date{
  font-family:'Syne',sans-serif;
  font-size:.68rem;letter-spacing:.15em;
  color:rgba(232,226,217,.3);
  text-transform:uppercase;
  padding-top:4px;
}
.exp-main{}
.exp-title{
  font-family:'Bebas Neue',sans-serif;
  font-size:clamp(28px,3.5vw,48px);
  letter-spacing:.02em;
  line-height:1;
  margin-bottom:8px;
}
.exp-org{
  font-size:.82rem;
  color:rgba(232,226,217,.4);
  letter-spacing:.08em;
  margin-bottom:16px;
}
.exp-desc{
  font-size:.9rem;line-height:1.7;
  color:rgba(232,226,217,.45);
  max-width:500px;
}
.exp-tag{
  font-family:'Syne',sans-serif;
  font-size:.6rem;letter-spacing:.2em;text-transform:uppercase;
  border:1px solid rgba(232,226,217,.12);
  padding:6px 14px;border-radius:100px;
  color:rgba(232,226,217,.4);
  white-space:nowrap;
  align-self:flex-start;
}

/* ─────────────────────────────────────────
   PROJECTS
───────────────────────────────────────── */
.projects{
  padding:120px 48px;
  border-bottom:1px solid rgba(232,226,217,.08);
}
.projects-list{margin-top:72px;display:flex;flex-direction:column;gap:1px;}
.project-item{
  display:grid;
  grid-template-columns:60px 1fr auto auto;
  align-items:center;gap:32px;
  padding:28px 0;
  border-top:1px solid rgba(232,226,217,.06);
  transition:all .35s cubic-bezier(.16,1,.3,1);
  position:relative;overflow:hidden;
  cursor:default;
}
.project-item::before{
  content:'';position:absolute;inset:0;left:-100%;
  background:rgba(232,226,217,.03);
  transition:left .5s cubic-bezier(.16,1,.3,1);
}
.project-item:hover::before{left:0;}
.project-item:hover{padding-left:20px;}

.proj-num{
  font-family:'Bebas Neue',sans-serif;
  font-size:2rem;color:rgba(232,226,217,.12);
}
.proj-name{
  font-family:'Syne',sans-serif;
  font-size:1.2rem;font-weight:700;
  transition:letter-spacing .35s;
}
.project-item:hover .proj-name{letter-spacing:.04em;}
.proj-desc{
  font-size:.85rem;
  color:rgba(232,226,217,.4);
  max-width:380px;
}
.proj-stack{
  display:flex;gap:8px;flex-wrap:wrap;justify-content:flex-end;
}
.proj-chip{
  font-size:.68rem;letter-spacing:.1em;
  background:rgba(232,226,217,.05);
  border:1px solid rgba(232,226,217,.1);
  padding:4px 12px;border-radius:2px;
  color:rgba(232,226,217,.5);
}
.proj-arrow{
  font-size:1.2rem;
  color:rgba(232,226,217,.2);
  transform:rotate(-45deg);
  transition:transform .3s,color .3s;
}
.project-item:hover .proj-arrow{transform:rotate(0);color:#e8e2d9;}

/* ─────────────────────────────────────────
   CONTACT
───────────────────────────────────────── */
.contact{
  padding:120px 48px 80px;
  text-align:center;
  position:relative;overflow:hidden;
}
.contact-big{
  font-family:'Bebas Neue',sans-serif;
  font-size:clamp(60px,11vw,160px);
  line-height:.88;
  letter-spacing:-.01em;
  margin:48px 0;
  transition:letter-spacing .4s;
}
.contact-big:hover{letter-spacing:.04em;}
.contact-big a{
  text-decoration:none;color:inherit;
  background:linear-gradient(90deg,#e8e2d9,rgba(232,226,217,.3));
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;
  background-size:200%;
  animation:gradShift 4s ease-in-out infinite alternate;
}
@keyframes gradShift{to{background-position:100%;}}

.contact-links{
  display:flex;justify-content:center;gap:40px;flex-wrap:wrap;
  margin-top:40px;
}
.contact-link{
  font-family:'Syne',sans-serif;
  font-size:.75rem;letter-spacing:.2em;text-transform:uppercase;
  color:rgba(232,226,217,.4);
  text-decoration:none;
  display:flex;align-items:center;gap:10px;
  transition:color .3s,gap .3s;
}
.contact-link::after{content:'↗';font-size:1rem;transition:transform .3s;}
.contact-link:hover{color:#e8e2d9;gap:14px;}
.contact-link:hover::after{transform:translate(3px,-3px);}

.contact-bg{
  position:absolute;inset:0;
  background:radial-gradient(ellipse 60% 60% at 50% 50%,rgba(255,255,255,.025),transparent);
  pointer-events:none;
}

/* ─────────────────────────────────────────
   FOOTER
───────────────────────────────────────── */
.footer{
  padding:24px 48px;
  border-top:1px solid rgba(232,226,217,.06);
  display:flex;justify-content:space-between;
  font-family:'Syne',sans-serif;
  font-size:.62rem;letter-spacing:.2em;text-transform:uppercase;
  color:rgba(232,226,217,.2);
}

/* ─────────────────────────────────────────
   REVEAL ANIMATION
───────────────────────────────────────── */
.reveal{
  opacity:0;transform:translateY(40px);
  transition:opacity .9s cubic-bezier(.16,1,.3,1),transform .9s cubic-bezier(.16,1,.3,1);
}
.reveal.visible{opacity:1;transform:translateY(0);}
.reveal-delay-1{transition-delay:.1s;}
.reveal-delay-2{transition-delay:.2s;}
.reveal-delay-3{transition-delay:.35s;}

/* ─── RESPONSIVE ─── */
@media(max-width:768px){
  .hero,.about,.skills,.experience,.projects,.contact,.footer{padding-left:24px;padding-right:24px;}
  .about{grid-template-columns:1fr;}
  .about-left{padding-right:0;margin-bottom:60px;}
  .about-right{padding-left:0;border-left:none;border-top:1px solid rgba(232,226,217,.08);padding-top:40px;}
  .skills-grid{grid-template-columns:1fr 1fr;}
  .exp-item{grid-template-columns:1fr;gap:12px;}
  .project-item{grid-template-columns:40px 1fr;gap:16px;}
  .proj-stack,.proj-arrow{display:none;}
  #cur,#cur-ring{display:none;}
}
</style>
</head>
<body>

<!-- CURSOR -->
<div id="cur"></div>
<div id="cur-ring"></div>

<!-- PARTICLE CANVAS -->
<canvas id="bgCanvas"></canvas>

<main class="page">

  <!-- ══════════════ HERO ══════════════ -->
  <section class="hero">
    <div class="hero-bg-letter">S</div>

    <nav class="nav">
      <div>
        <span class="status-dot"></span>Available for work
      </div>
      <div class="nav-links">
        <a href="#about">About</a>
        <a href="#skills">Skills</a>
        <a href="#experience">Experience</a>
        <a href="#projects">Projects</a>
        <a href="#contact">Contact</a>
      </div>
      <div>Tamil Nadu, IN &nbsp;·&nbsp; 2026</div>
    </nav>

    <div class="hero-center">
      <div class="hero-eyebrow">Java Full Stack Developer</div>
      <h1 class="hero-name">
        <span class="line"><span>SANJAI</span></span>
        <span class="line"><span>ARIVALAGAN</span></span>
      </h1>
      <div class="hero-sub">
        <div class="hero-role-pill">React · Spring Boot · Java</div>
        <p class="hero-desc">Building scalable web applications that live at the intersection of clean architecture and refined UI.</p>
      </div>
    </div>

    <div class="hero-bottom">
      <div class="scroll-hint">
        <span class="scroll-line"></span>
        Scroll to explore
      </div>
      <div class="location-tag">📍 Tamil Nadu, India</div>
    </div>
  </section>

  <!-- ══ MARQUEE ══ -->
  <div class="marquee-wrap">
    <div class="marquee-track">
      <span>Java</span><span class="accent">✦</span>
      <span>Spring Boot</span><span class="accent">✦</span>
      <span>React</span><span class="accent">✦</span>
      <span>Full Stack</span><span class="accent">✦</span>
      <span>MySQL</span><span class="accent">✦</span>
      <span>REST API</span><span class="accent">✦</span>
      <span>JavaScript</span><span class="accent">✦</span>
      <span>Web Developer</span><span class="accent">✦</span>
      <span>Java</span><span class="accent">✦</span>
      <span>Spring Boot</span><span class="accent">✦</span>
      <span>React</span><span class="accent">✦</span>
      <span>Full Stack</span><span class="accent">✦</span>
      <span>MySQL</span><span class="accent">✦</span>
      <span>REST API</span><span class="accent">✦</span>
      <span>JavaScript</span><span class="accent">✦</span>
      <span>Web Developer</span><span class="accent">✦</span>
    </div>
  </div>

  <!-- ══════════════ ABOUT ══════════════ -->
  <section id="about" class="about">
    <div class="about-left reveal">
      <div class="section-num">01 — About</div>
      <h2 class="big-heading">
        WHO<br/><em>I AM</em>
      </h2>
    </div>
    <div class="about-right reveal reveal-delay-2">
      <p class="about-text">
        I'm a <strong>Java Full Stack Developer</strong> based in Tamil Nadu, India — currently an intern at <strong>Test Yantra</strong>, building production-grade web systems with Spring Boot backends and React frontends.<br/><br/>
        I believe great software is invisible — it just <strong>works</strong>. Clean APIs, thoughtful architecture, and interfaces that feel effortless.
      </p>
      <div class="yaml-block">
        <span class="c"># identity.yaml</span><br/>
        <span class="k">name</span>: <span class="s">"Sanjai Arivalagan"</span><br/>
        <span class="k">role</span>: <span class="s">"Java Full Stack Developer"</span><br/>
        <span class="k">base</span>: <span class="s">"Tamil Nadu, IN"</span><br/>
        <span class="k">focus</span>: <span class="v">[ backend, web, systems ]</span><br/>
        <span class="k">status</span>: <span class="s">"open to opportunities"</span><br/>
        <span class="k">learning</span>: <span class="s">"Microservices, System Design"</span>
      </div>
    </div>
  </section>

  <!-- ══════════════ SKILLS ══════════════ -->
  <section id="skills" class="skills">
    <div class="skills-header reveal">
      <div>
        <div class="section-num">02 — Skills</div>
        <h2 class="big-heading">TECH<br/><em>STACK</em></h2>
      </div>
      <p style="max-width:280px;font-size:.9rem;color:rgba(232,226,217,.4);line-height:1.7;">
        Hover each category to see proficiency levels built through real projects.
      </p>
    </div>
    <div class="skills-grid reveal reveal-delay-1">
      <div class="skill-cell">
        <div class="skill-cell-label">Backend</div>
        <div class="skill-items">
          <div class="skill-item">Java<div class="skill-bar-mini"><div class="skill-bar-fill" style="width:90%"></div></div></div>
          <div class="skill-item">Spring Boot<div class="skill-bar-mini"><div class="skill-bar-fill" style="width:82%"></div></div></div>
          <div class="skill-item">Spring MVC<div class="skill-bar-mini"><div class="skill-bar-fill" style="width:78%"></div></div></div>
          <div class="skill-item">Hibernate<div class="skill-bar-mini"><div class="skill-bar-fill" style="width:75%"></div></div></div>
          <div class="skill-item">REST API<div class="skill-bar-mini"><div class="skill-bar-fill" style="width:88%"></div></div></div>
        </div>
      </div>
      <div class="skill-cell">
        <div class="skill-cell-label">Frontend</div>
        <div class="skill-items">
          <div class="skill-item">React<div class="skill-bar-mini"><div class="skill-bar-fill" style="width:78%"></div></div></div>
          <div class="skill-item">JavaScript<div class="skill-bar-mini"><div class="skill-bar-fill" style="width:82%"></div></div></div>
          <div class="skill-item">HTML / CSS<div class="skill-bar-mini"><div class="skill-bar-fill" style="width:90%"></div></div></div>
          <div class="skill-item">Tailwind CSS<div class="skill-bar-mini"><div class="skill-bar-fill" style="width:75%"></div></div></div>
        </div>
      </div>
      <div class="skill-cell">
        <div class="skill-cell-label">Database</div>
        <div class="skill-items">
          <div class="skill-item">MySQL<div class="skill-bar-mini"><div class="skill-bar-fill" style="width:80%"></div></div></div>
          <div class="skill-item">PostgreSQL<div class="skill-bar-mini"><div class="skill-bar-fill" style="width:68%"></div></div></div>
          <div class="skill-item">MongoDB<div class="skill-bar-mini"><div class="skill-bar-fill" style="width:60%"></div></div></div>
        </div>
      </div>
      <div class="skill-cell">
        <div class="skill-cell-label">Tools & DevOps</div>
        <div class="skill-items">
          <div class="skill-item">Git / GitHub<div class="skill-bar-mini"><div class="skill-bar-fill" style="width:85%"></div></div></div>
          <div class="skill-item">Maven<div class="skill-bar-mini"><div class="skill-bar-fill" style="width:72%"></div></div></div>
          <div class="skill-item">Postman<div class="skill-bar-mini"><div class="skill-bar-fill" style="width:80%"></div></div></div>
          <div class="skill-item">IntelliJ IDEA<div class="skill-bar-mini"><div class="skill-bar-fill" style="width:88%"></div></div></div>
        </div>
      </div>
    </div>
  </section>

  <!-- ══════════════ EXPERIENCE ══════════════ -->
  <section id="experience" class="experience">
    <div class="section-num reveal">03 — Experience</div>
    <h2 class="big-heading reveal reveal-delay-1">WHERE<br/><em>I'VE WORKED</em></h2>
    <div class="exp-list">
      <div class="exp-item reveal">
        <div class="exp-date">2024 — Present</div>
        <div class="exp-main">
          <div class="exp-title">Java Full Stack Intern</div>
          <div class="exp-org">Test Yantra Software Solutions</div>
          <div class="exp-desc">Building enterprise web applications with Spring Boot microservices and React frontends. Involved in API design, database schema optimization, and deployment workflows.</div>
        </div>
        <div class="exp-tag">Current</div>
      </div>
      <div class="exp-item reveal reveal-delay-1">
        <div class="exp-date">2020 — 2024</div>
        <div class="exp-main">
          <div class="exp-title">B.E. Computer Science & Engineering</div>
          <div class="exp-org">Tamil Nadu, India</div>
          <div class="exp-desc">Strong academic foundation in data structures, OOP, DBMS, computer networks, and software engineering principles.</div>
        </div>
        <div class="exp-tag">Graduated</div>
      </div>
    </div>
  </section>

  <!-- ══════════════ PROJECTS ══════════════ -->
  <section id="projects" class="projects">
    <div class="section-num reveal">04 — Projects</div>
    <h2 class="big-heading reveal reveal-delay-1">SELECTED<br/><em>WORK</em></h2>
    <div class="projects-list">
      <div class="project-item reveal">
        <div class="proj-num">01</div>
        <div>
          <div class="proj-name">E-Commerce Platform</div>
          <div class="proj-desc">Full-stack shopping system with product management, cart, and secure payment flow.</div>
        </div>
        <div class="proj-stack">
          <span class="proj-chip">Spring Boot</span>
          <span class="proj-chip">React</span>
          <span class="proj-chip">MySQL</span>
        </div>
        <div class="proj-arrow">↗</div>
      </div>
      <div class="project-item reveal reveal-delay-1">
        <div class="proj-num">02</div>
        <div>
          <div class="proj-name">Task Management API</div>
          <div class="proj-desc">RESTful API with JWT auth, RBAC, and real-time task tracking.</div>
        </div>
        <div class="proj-stack">
          <span class="proj-chip">Java</span>
          <span class="proj-chip">Spring Security</span>
          <span class="proj-chip">JWT</span>
        </div>
        <div class="proj-arrow">↗</div>
      </div>
      <div class="project-item reveal reveal-delay-2">
        <div class="proj-num">03</div>
        <div>
          <div class="proj-name">Developer Portfolio</div>
          <div class="proj-desc">Animated personal portfolio deployed on Netlify with CI/CD pipeline.</div>
        </div>
        <div class="proj-stack">
          <span class="proj-chip">React</span>
          <span class="proj-chip">Tailwind</span>
          <span class="proj-chip">Netlify</span>
        </div>
        <div class="proj-arrow">↗</div>
      </div>
    </div>
  </section>

  <!-- ══════════════ CONTACT ══════════════ -->
  <section id="contact" class="contact">
    <div class="contact-bg"></div>
    <div class="section-num reveal">05 — Contact</div>
    <div class="contact-big reveal reveal-delay-1">
      <a href="mailto:sanjaiarivu03@gmail.com">LET'S<br/>TALK.</a>
    </div>
    <div class="contact-links reveal reveal-delay-2">
      <a class="contact-link" href="https://portfolio-sanjai-2026.netlify.app" target="_blank">Portfolio</a>
      <a class="contact-link" href="https://www.linkedin.com/in/sanjaiarivu03" target="_blank">LinkedIn</a>
      <a class="contact-link" href="mailto:sanjaiarivu03@gmail.com">Gmail</a>
      <a class="contact-link" href="https://github.com/sanjai03" target="_blank">GitHub</a>
    </div>
  </section>

  <!-- ══ FOOTER ══ -->
  <footer class="footer">
    <span>Sanjai Arivalagan © 2026</span>
    <span>Java Full Stack Developer</span>
    <span>Tamil Nadu, India</span>
  </footer>

</main>

<script>
/* ─── CURSOR ─── */
const cur = document.getElementById('cur');
const ring = document.getElementById('cur-ring');
let mx=0,my=0,rx=0,ry=0;
document.addEventListener('mousemove',e=>{mx=e.clientX;my=e.clientY;cur.style.left=mx+'px';cur.style.top=my+'px';});
(function animRing(){rx+=(mx-rx)*.12;ry+=(my-ry)*.12;ring.style.left=rx+'px';ring.style.top=ry+'px';requestAnimationFrame(animRing);})();

/* ─── PARTICLE CANVAS ─── */
const canvas=document.getElementById('bgCanvas');
const ctx=canvas.getContext('2d');
let W,H,particles=[];

function resize(){W=canvas.width=window.innerWidth;H=canvas.height=window.innerHeight;}
resize();window.addEventListener('resize',resize);

class Particle{
  constructor(){this.reset();}
  reset(){
    this.x=Math.random()*W;
    this.y=Math.random()*H;
    this.size=Math.random()*1.5+.2;
    this.alpha=Math.random()*.5+.1;
    this.vx=(Math.random()-.5)*.15;
    this.vy=(Math.random()-.5)*.15;
    this.life=0;this.maxLife=Math.random()*400+200;
  }
  update(){
    this.x+=this.vx;this.y+=this.vy;this.life++;
    if(this.life>this.maxLife||this.x<0||this.x>W||this.y<0||this.y>H) this.reset();
  }
  draw(){
    const progress=this.life/this.maxLife;
    const fade=progress<.1?progress/.1:progress>.8?(1-progress)/.2:1;
    ctx.globalAlpha=this.alpha*fade;
    ctx.fillStyle='#e8e2d9';
    ctx.beginPath();ctx.arc(this.x,this.y,this.size,0,Math.PI*2);ctx.fill();
  }
}

for(let i=0;i<120;i++) particles.push(new Particle());

function drawConnections(){
  for(let i=0;i<particles.length;i++){
    for(let j=i+1;j<particles.length;j++){
      const dx=particles[i].x-particles[j].x;
      const dy=particles[i].y-particles[j].y;
      const dist=Math.sqrt(dx*dx+dy*dy);
      if(dist<90){
        ctx.globalAlpha=(.06*(1-dist/90));
        ctx.strokeStyle='#e8e2d9';
        ctx.lineWidth=.5;
        ctx.beginPath();
        ctx.moveTo(particles[i].x,particles[i].y);
        ctx.lineTo(particles[j].x,particles[j].y);
        ctx.stroke();
      }
    }
  }
}

function animate(){
  ctx.clearRect(0,0,W,H);
  particles.forEach(p=>{p.update();p.draw();});
  drawConnections();
  ctx.globalAlpha=1;
  requestAnimationFrame(animate);
}
animate();

/* ─── SCROLL REVEAL ─── */
const reveals=document.querySelectorAll('.reveal');
const observer=new IntersectionObserver(entries=>{
  entries.forEach(e=>{if(e.isIntersecting){e.target.classList.add('visible');}});
},{threshold:.12});
reveals.forEach(el=>observer.observe(el));

/* ─── MAGNETIC LINKS ─── */
document.querySelectorAll('.contact-link,.badge').forEach(el=>{
  el.addEventListener('mousemove',e=>{
    const r=el.getBoundingClientRect();
    const dx=e.clientX-r.left-r.width/2;
    const dy=e.clientY-r.top-r.height/2;
    el.style.transform=`translate(${dx*.12}px,${dy*.12}px)`;
  });
  el.addEventListener('mouseleave',()=>{el.style.transform='';});
});
</script>
</body>
</html>
