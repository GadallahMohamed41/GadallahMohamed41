<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<style>
@import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@300;400;700;800&family=Space+Grotesk:wght@300;400;600;700&display=swap');
*{margin:0;padding:0;box-sizing:border-box}
:root{--g1:#00ff87;--g2:#00c9ff;--dark:#060810;--card:#0b0f1e;--border:#151d35}
body{background:var(--dark);color:#e2e8f0;font-family:'Space Grotesk',sans-serif;overflow-x:hidden}
#cv{position:fixed;inset:0;z-index:0}
.pg{position:relative;z-index:2;max-width:920px;margin:0 auto;padding:0 1.5rem 4rem}

.hero{min-height:100vh;display:flex;flex-direction:column;align-items:center;justify-content:center;text-align:center;padding:1rem}
.orb{position:absolute;width:400px;height:400px;border-radius:50%;background:radial-gradient(circle,#00ff8715 0%,#00c9ff08 50%,transparent 70%);filter:blur(40px);animation:orbPulse 4s ease-in-out infinite;pointer-events:none}
.hero-tag{font-family:'JetBrains Mono',monospace;font-size:.7rem;letter-spacing:4px;color:var(--g1);text-transform:uppercase;margin-bottom:1rem;opacity:0;animation:fadeUp .6s .2s forwards}
.hero-name{font-family:'Space Grotesk',sans-serif;font-size:clamp(2.8rem,7vw,5rem);font-weight:700;line-height:1.05;margin-bottom:.4rem;position:relative}
.hero-name .letter{display:inline-block;opacity:0;transform:translateY(40px) rotateX(-90deg);background:linear-gradient(135deg,#fff 0%,var(--g1) 60%,var(--g2) 100%);-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text}
.hero-name .sp{display:inline-block;width:.4em}
.hero-role{font-family:'JetBrains Mono',monospace;font-size:clamp(.8rem,2vw,1rem);color:var(--g2);margin-bottom:1.5rem;opacity:0;animation:fadeUp .6s .8s forwards;letter-spacing:1px}
.typing-box{background:#0b0f1e;border:1px solid var(--border);border-radius:10px;padding:.65rem 1.2rem;font-family:'JetBrains Mono',monospace;font-size:.82rem;color:#aaa;margin-bottom:1.5rem;opacity:0;animation:fadeUp .6s 1s forwards;display:inline-block;min-width:320px;text-align:left}
.typing-box .prompt{color:var(--g1)}
.typing-box .cursor{display:inline-block;width:8px;height:1em;background:var(--g1);vertical-align:middle;margin-left:2px;animation:blink .7s step-end infinite}
.badge-row{display:flex;gap:8px;flex-wrap:wrap;justify-content:center;opacity:0;animation:fadeUp .6s 1.2s forwards}
.badge{display:inline-flex;align-items:center;gap:6px;padding:6px 14px;border-radius:7px;font-family:'JetBrains Mono',monospace;font-size:.7rem;border:1px solid var(--border);background:#0b0f1e;color:#aaa;cursor:pointer;transition:all .25s;text-decoration:none;position:relative;overflow:hidden}
.badge::before{content:'';position:absolute;inset:0;background:linear-gradient(135deg,var(--g1),var(--g2));opacity:0;transition:.25s}
.badge:hover::before{opacity:.12}
.badge:hover{border-color:var(--g1);color:var(--g1);transform:translateY(-2px);box-shadow:0 6px 20px #00ff8720}
.badge span{position:relative;z-index:1}
.pulse{width:6px;height:6px;border-radius:50%;background:var(--g1);animation:pulse 1.5s ease infinite;flex-shrink:0}

.sec{padding:3rem 0 0;opacity:0;transform:translateY(24px);transition:opacity .7s,transform .7s}
.sec.visible{opacity:1;transform:translateY(0)}
.sec-header{display:flex;align-items:center;gap:12px;margin-bottom:1.5rem}
.sec-num{font-family:'JetBrains Mono',monospace;font-size:.63rem;color:var(--g1);letter-spacing:2px}
.sec-title{font-size:1.2rem;font-weight:700;color:#fff}
.sec-line{flex:1;height:1px;background:linear-gradient(90deg,var(--border),transparent)}

.code-card{background:#060810;border:1px solid var(--border);border-radius:12px;overflow:hidden;box-shadow:0 20px 60px #00000080}
.code-topbar{display:flex;align-items:center;gap:7px;padding:10px 14px;background:#0b0f1e;border-bottom:1px solid var(--border)}
.dot{width:11px;height:11px;border-radius:50%}
.dr{background:#ff5f56}.dy{background:#ffbd2e}.dg{background:#27c93f}
.code-fname{font-family:'JetBrains Mono',monospace;font-size:.68rem;color:#4a5568;margin-left:auto}
.code-body{padding:1.2rem 1.5rem;font-family:'JetBrains Mono',monospace;font-size:.77rem;line-height:2;overflow-x:auto}
.ln{color:#2d3748;margin-right:18px;font-size:.63rem;user-select:none}
.kw{color:#ff79c6}.cls{color:#50fa7b}.fn{color:#8be9fd}.str{color:#f1fa8c}.prop{color:#bd93f9}.cmt{color:#4a5568;font-style:italic}

.skills-wrap{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:.75rem}
.sk-card{background:var(--card);border:1px solid var(--border);border-radius:10px;padding:1rem 1.1rem;transition:all .3s;position:relative;overflow:hidden;cursor:default}
.sk-card::after{content:'';position:absolute;bottom:0;left:0;right:0;height:2px;background:linear-gradient(90deg,var(--g1),var(--g2));transform:scaleX(0);transform-origin:left;transition:.3s}
.sk-card:hover{transform:translateY(-3px);border-color:#1e2d50;box-shadow:0 10px 30px #00ff8712}
.sk-card:hover::after{transform:scaleX(1)}
.sk-head{display:flex;align-items:center;gap:8px;margin-bottom:10px}
.sk-emoji{font-size:1.2rem}
.sk-label{font-family:'JetBrains Mono',monospace;font-size:.65rem;color:var(--g1);letter-spacing:1.5px;text-transform:uppercase}
.sk-pills{display:flex;flex-wrap:wrap;gap:4px}
.pill{font-size:.65rem;font-family:'JetBrains Mono',monospace;padding:2px 8px;border-radius:4px;border:1px solid var(--border);color:#6e7681;transition:.2s}
.sk-card:hover .pill{border-color:#1e3a5a;color:#a0aec0}

.proj-grid{display:grid;grid-template-columns:1fr 1fr;gap:.75rem}
.proj{background:var(--card);border:1px solid var(--border);border-radius:10px;padding:1.1rem;transition:all .3s;position:relative;overflow:hidden;cursor:default}
.proj-glow{position:absolute;inset:0;background:radial-gradient(circle at 50% 0%,#00ff8708,transparent 60%);opacity:0;transition:.3s}
.proj:hover .proj-glow{opacity:1}
.proj:hover{transform:translateY(-4px);box-shadow:0 16px 40px #00000060;border-color:#1e3a5a}
.proj-top{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:.6rem}
.proj-icon{font-size:1.4rem}
.proj-year{font-family:'JetBrains Mono',monospace;font-size:.62rem;color:var(--g1);background:#00ff8710;border:1px solid #00ff8725;padding:2px 8px;border-radius:4px}
.proj-name{font-size:.88rem;font-weight:700;color:#fff;margin-bottom:.4rem}
.proj-desc{font-size:.73rem;color:#6e7681;line-height:1.65;margin-bottom:.8rem}
.proj-tags{display:flex;flex-wrap:wrap;gap:4px}
.ptag{font-size:.62rem;font-family:'JetBrains Mono',monospace;padding:2px 8px;border-radius:4px;background:#00c9ff08;border:1px solid #00c9ff20;color:var(--g2)}

.stats-row{display:grid;grid-template-columns:repeat(3,1fr);gap:.75rem}
.stat{background:var(--card);border:1px solid var(--border);border-radius:10px;padding:1.1rem;text-align:center;transition:.3s;cursor:default;position:relative;overflow:hidden}
.stat::before{content:'';position:absolute;inset:0;background:radial-gradient(circle at 50% 100%,#00ff8710,transparent 60%);opacity:0;transition:.3s}
.stat:hover::before{opacity:1}
.stat:hover{transform:translateY(-3px);border-color:var(--g1);box-shadow:0 0 24px #00ff8720}
.stat-num{font-family:'JetBrains Mono',monospace;font-size:2.2rem;font-weight:800;background:linear-gradient(135deg,var(--g1),var(--g2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text}
.stat-lbl{font-size:.68rem;color:#4a5568;font-family:'JetBrains Mono',monospace;margin-top:4px;letter-spacing:1px}

.exp{background:var(--card);border:1px solid var(--border);border-radius:10px;padding:1.25rem;display:flex;gap:1rem;transition:.3s}
.exp:hover{border-color:var(--g1);box-shadow:0 0 24px #00ff8715}
.exp-left{display:flex;flex-direction:column;align-items:center;padding-top:4px}
.exp-dot{width:12px;height:12px;border-radius:50%;background:var(--g1);box-shadow:0 0 10px var(--g1),0 0 20px var(--g1);animation:glowPulse 2s ease infinite;flex-shrink:0}
.exp-vert{flex:1;width:2px;background:linear-gradient(180deg,var(--g1),transparent);margin-top:6px;border-radius:2px}
.exp-role{font-size:.95rem;font-weight:700;color:#fff;margin-bottom:.2rem}
.exp-org{font-family:'JetBrains Mono',monospace;font-size:.7rem;color:var(--g1);margin-bottom:.5rem;letter-spacing:.5px}
.exp-period{font-family:'JetBrains Mono',monospace;font-size:.62rem;background:#00ff8710;border:1px solid #00ff8725;color:var(--g1);padding:2px 9px;border-radius:4px;display:inline-block;margin-bottom:.7rem}
.exp-li{font-size:.75rem;color:#6e7681;line-height:1.8;padding-left:.9rem;position:relative}
.exp-li::before{content:'▸';position:absolute;left:0;color:var(--g1)}

.cert-list{display:flex;flex-direction:column;gap:.5rem}
.cert{display:flex;align-items:center;gap:12px;background:var(--card);border:1px solid var(--border);border-radius:9px;padding:.8rem 1.1rem;transition:all .25s;cursor:default}
.cert:hover{border-color:var(--g1);padding-left:1.5rem;box-shadow:0 0 16px #00ff8712}
.cert-ico{font-size:1.2rem;flex-shrink:0}
.cert-name{font-size:.82rem;font-weight:600;color:#e2e8f0}
.cert-by{font-family:'JetBrains Mono',monospace;font-size:.66rem;color:#4a5568;margin-top:2px}
.cert-tag{margin-left:auto;font-family:'JetBrains Mono',monospace;font-size:.6rem;background:#00ff8712;border:1px solid #00ff8730;color:var(--g1);padding:2px 9px;border-radius:4px;white-space:nowrap}

.copy-wrap{margin-top:3rem;text-align:center}
.copy-btn{display:inline-flex;align-items:center;gap:10px;padding:12px 32px;background:linear-gradient(135deg,var(--g1),var(--g2));border:none;border-radius:10px;font-family:'JetBrains Mono',monospace;font-size:.85rem;font-weight:700;color:#060810;cursor:pointer;transition:all .25s;box-shadow:0 0 24px #00ff8740}
.copy-btn:hover{transform:scale(1.05);box-shadow:0 0 40px #00ff8760}
.copy-btn:active{transform:scale(.97)}

.footer{text-align:center;padding-top:2rem}
.footer-card{display:inline-flex;align-items:center;gap:1.2rem;background:var(--card);border:1px solid var(--border);border-radius:10px;padding:.85rem 1.8rem;font-family:'JetBrains Mono',monospace;font-size:.72rem;color:#4a5568}
.footer-card span{color:var(--g1)}
.sep{color:var(--border)}

.scroll-top{position:fixed;bottom:1.5rem;right:1.5rem;z-index:100;width:40px;height:40px;border-radius:9px;background:linear-gradient(135deg,var(--g1),var(--g2));border:none;cursor:pointer;font-size:1rem;display:flex;align-items:center;justify-content:center;box-shadow:0 0 16px #00ff8740;transition:all .2s;opacity:0;pointer-events:none}
.scroll-top.show{opacity:1;pointer-events:all}
.scroll-top:hover{transform:scale(1.1)}

.toast{position:fixed;bottom:1.5rem;left:50%;transform:translateX(-50%) translateY(80px);background:var(--g1);color:#060810;font-family:'JetBrains Mono',monospace;font-size:.8rem;font-weight:700;padding:.65rem 1.5rem;border-radius:8px;transition:transform .35s cubic-bezier(.34,1.56,.64,1);z-index:999;pointer-events:none}
.toast.show{transform:translateX(-50%) translateY(0)}

@keyframes fadeUp{from{opacity:0;transform:translateY(16px)}to{opacity:1;transform:translateY(0)}}
@keyframes blink{50%{opacity:0}}
@keyframes pulse{0%,100%{opacity:1;transform:scale(1)}50%{opacity:.4;transform:scale(.7)}}
@keyframes orbPulse{0%,100%{transform:scale(1);opacity:.6}50%{transform:scale(1.2);opacity:1}}
@keyframes glowPulse{0%,100%{box-shadow:0 0 8px var(--g1)}50%{box-shadow:0 0 20px var(--g1),0 0 40px var(--g2)}}
@keyframes letterIn{from{opacity:0;transform:translateY(40px) rotateX(-90deg)}to{opacity:1;transform:translateY(0) rotateX(0)}}
</style>
</head>
<body>
<canvas id="cv"></canvas>
<button class="scroll-top" id="stBtn" onclick="window.scrollTo({top:0,behavior:'smooth'})">↑</button>
<div class="toast" id="toast">✅ Copied! Paste it on GitHub</div>

<div class="pg">

<div class="hero">
  <div class="orb"></div>
  <div class="hero-tag">⚡ Flutter Developer · Egypt</div>
  <div class="hero-name" id="heroName"></div>
  <div class="hero-role" id="heroRole"></div>
  <div class="typing-box"><span class="prompt">$ </span><span id="typingText"></span><span class="cursor"></span></div>
  <div class="badge-row">
    <a class="badge" href="https://github.com/GadallahMohamed41"><span class="pulse"></span><span>GitHub</span></a>
    <a class="badge" href="https://linkedin.com/in/gadallah-mohamed"><span class="pulse" style="background:var(--g2)"></span><span>LinkedIn</span></a>
    <a class="badge" href="mailto:goodashalaa912@gmail.com"><span class="pulse" style="background:#bf5af2"></span><span>goodashalaa912@gmail.com</span></a>
    <span class="badge" style="border-color:#00ff8730;color:var(--g1)"><span class="pulse"></span><span>Open to Remote 🌐</span></span>
  </div>
</div>

<div class="sec" data-sec>
  <div class="sec-header"><span class="sec-num">01</span><span class="sec-title">About</span><div class="sec-line"></div></div>
  <div class="code-card">
    <div class="code-topbar"><div class="dot dr"></div><div class="dot dy"></div><div class="dot dg"></div><span class="code-fname">about_me.dart</span></div>
    <div class="code-body" id="codeBody"><span class="cmt">// initializing...</span></div>
  </div>
</div>

<div class="sec" data-sec>
  <div class="sec-header"><span class="sec-num">02</span><span class="sec-title">Tech Stack</span><div class="sec-line"></div></div>
  <div class="skills-wrap">
    <div class="sk-card"><div class="sk-head"><span class="sk-emoji">📱</span><span class="sk-label">Mobile</span></div><div class="sk-pills"><span class="pill">Flutter</span><span class="pill">Dart</span><span class="pill">Android</span></div></div>
    <div class="sk-card"><div class="sk-head"><span class="sk-emoji">🏗</span><span class="sk-label">Architecture</span></div><div class="sk-pills"><span class="pill">Clean Arch</span><span class="pill">MVVM</span><span class="pill">BLoC</span><span class="pill">Provider</span></div></div>
    <div class="sk-card"><div class="sk-head"><span class="sk-emoji">☁️</span><span class="sk-label">Backend</span></div><div class="sk-pills"><span class="pill">Firebase</span><span class="pill">REST API</span><span class="pill">SQLite</span><span class="pill">FCM</span></div></div>
    <div class="sk-card"><div class="sk-head"><span class="sk-emoji">🤖</span><span class="sk-label">AI & IoT</span></div><div class="sk-pills"><span class="pill">OpenCV</span><span class="pill">Arduino</span><span class="pill">Bluetooth</span><span class="pill">Wi-Fi</span></div></div>
    <div class="sk-card"><div class="sk-head"><span class="sk-emoji">💻</span><span class="sk-label">Languages</span></div><div class="sk-pills"><span class="pill">C++</span><span class="pill">Java</span><span class="pill">Python</span><span class="pill">Assembly</span></div></div>
    <div class="sk-card"><div class="sk-head"><span class="sk-emoji">🛠</span><span class="sk-label">Tools</span></div><div class="sk-pills"><span class="pill">Git</span><span class="pill">GitHub</span><span class="pill">VS Code</span><span class="pill">Android Studio</span></div></div>
  </div>
</div>

<div class="sec" data-sec>
  <div class="sec-header"><span class="sec-num">03</span><span class="sec-title">Projects</span><div class="sec-line"></div></div>
  <div class="proj-grid">
    <div class="proj"><div class="proj-glow"></div><div class="proj-top"><span class="proj-icon">🦾</span><span class="proj-year">2026</span></div><div class="proj-name">Robotic Arm Control System</div><div class="proj-desc">IoT Flutter app for real-time wireless control of a physical robotic arm. Mobile & Desktop. Bluetooth + Wi-Fi, movement recording, emergency stop.</div><div class="proj-tags"><span class="ptag">Flutter</span><span class="ptag">Arduino</span><span class="ptag">Bluetooth</span><span class="ptag">IoT</span></div></div>
    <div class="proj"><div class="proj-glow"></div><div class="proj-top"><span class="proj-icon">✈️</span><span class="proj-year">2025</span></div><div class="proj-name">Travel & Booking App</div><div class="proj-desc">Full-featured travel app — smart search, wishlist, multiple payment methods, dark mode. Built on Clean Architecture with BLoC.</div><div class="proj-tags"><span class="ptag">Flutter</span><span class="ptag">BLoC</span><span class="ptag">REST API</span><span class="ptag">Clean Arch</span></div></div>
    <div class="proj"><div class="proj-glow"></div><div class="proj-top"><span class="proj-icon">🔒</span><span class="proj-year">2024</span></div><div class="proj-name">Smart Security App</div><div class="proj-desc">Real-time Flutter app for IoT-based home security — live alerts and remote control with Firebase push notifications.</div><div class="proj-tags"><span class="ptag">Flutter</span><span class="ptag">Firebase</span><span class="ptag">IoT</span><span class="ptag">FCM</span></div></div>
    <div class="proj"><div class="proj-glow"></div><div class="proj-top"><span class="proj-icon">🏦</span><span class="proj-year">2023</span></div><div class="proj-name">Banking App</div><div class="proj-desc">Secure Flutter banking app with SQLite, transactional balance transfers, and clean financial UI design.</div><div class="proj-tags"><span class="ptag">Flutter</span><span class="ptag">SQLite</span><span class="ptag">Dart</span></div></div>
  </div>
</div>

<div class="sec" data-sec>
  <div class="sec-header"><span class="sec-num">04</span><span class="sec-title">Stats</span><div class="sec-line"></div></div>
  <div class="stats-row">
    <div class="stat"><div class="stat-num" id="s1">0+</div><div class="stat-lbl">Projects Shipped</div></div>
    <div class="stat"><div class="stat-num" id="s2">0+</div><div class="stat-lbl">Years Flutter</div></div>
    <div class="stat"><div class="stat-num">Top 3</div><div class="stat-lbl">GAIC Program</div></div>
  </div>
</div>

<div class="sec" data-sec>
  <div class="sec-header"><span class="sec-num">05</span><span class="sec-title">Experience</span><div class="sec-line"></div></div>
  <div class="exp">
    <div class="exp-left"><div class="exp-dot"></div><div class="exp-vert"></div></div>
    <div>
      <div class="exp-role">Flutter Teaching Assistant</div>
      <div class="exp-org">// TechUP Academy</div>
      <span class="exp-period">Dec 2025 → Present</span>
      <div class="exp-li">Delivered Flutter & Dart sessions alongside senior instructors</div>
      <div class="exp-li">Debugged live code and guided students through hands-on projects</div>
      <div class="exp-li">Simplified complex concepts and gave structured feedback on assignments</div>
    </div>
  </div>
</div>

<div class="sec" data-sec>
  <div class="sec-header"><span class="sec-num">06</span><span class="sec-title">Certifications</span><div class="sec-line"></div></div>
  <div class="cert-list">
    <div class="cert"><span class="cert-ico">🥇</span><div><div class="cert-name">Top 3 Achiever — GAIC Program</div><div class="cert-by">EU-funded · National Council for Women</div></div><span class="cert-tag">Award</span></div>
    <div class="cert"><span class="cert-ico">📜</span><div><div class="cert-name">Mobile App Development Diploma</div><div class="cert-by">Information Technology Institute (ITI)</div></div></div>
    <div class="cert"><span class="cert-ico">📜</span><div><div class="cert-name">SprintUp — Mobile Development by Flutter</div><div class="cert-by">Sprints</div></div></div>
    <div class="cert"><span class="cert-ico">📜</span><div><div class="cert-name">Flutter Program — 60 hrs</div><div class="cert-by">Creativa Innovation Hub · ITIDA · TIEC · MOR</div></div></div>
  </div>
</div>

<div class="copy-wrap">
  <button class="copy-btn" id="copyBtn" onclick="copyReadme()">
    <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><rect x="9" y="9" width="13" height="13" rx="2"/><path d="M5 15H4a2 2 0 01-2-2V4a2 2 0 012-2h9a2 2 0 012 2v1"/></svg>
    Copy README for GitHub
  </button>
</div>

<div class="footer">
  <div class="footer-card">
    <span>🇸🇦 Arabic</span><span class="sep">|</span>
    <span>🇬🇧 English B2</span><span class="sep">|</span>
    <span>🌐 Open for Remote</span><span class="sep">|</span>
    <span style="color:#4a5568">Beheira, Egypt</span>
  </div>
</div>

</div>

<script>
const cv=document.getElementById('cv'),ctx=cv.getContext('2d');
function rsz(){cv.width=window.innerWidth;cv.height=window.innerHeight}rsz();
window.addEventListener('resize',rsz);
const pts=Array.from({length:65},()=>({x:Math.random()*innerWidth,y:Math.random()*innerHeight,vx:(Math.random()-.5)*.25,vy:(Math.random()-.5)*.25,r:Math.random()*1.2+.3,c:Math.random()>.5?'#00ff87':'#00c9ff'}));
function drawPts(){ctx.clearRect(0,0,cv.width,cv.height);pts.forEach(p=>{p.x+=p.vx;p.y+=p.vy;if(p.x<0||p.x>cv.width)p.vx*=-1;if(p.y<0||p.y>cv.height)p.vy*=-1;ctx.beginPath();ctx.arc(p.x,p.y,p.r,0,Math.PI*2);ctx.fillStyle=p.c;ctx.fill();});pts.forEach((a,i)=>pts.slice(i+1).forEach(b=>{const d=Math.hypot(a.x-b.x,a.y-b.y);if(d<110){ctx.beginPath();ctx.moveTo(a.x,a.y);ctx.lineTo(b.x,b.y);ctx.strokeStyle=`rgba(0,255,135,${.12*(1-d/110)})`;ctx.lineWidth=.5;ctx.stroke();}}));requestAnimationFrame(drawPts);}drawPts();

const style=document.createElement('style');style.textContent=`@keyframes letterIn{from{opacity:0;transform:translateY(40px) rotateX(-90deg)}to{opacity:1;transform:translateY(0) rotateX(0)}}`;document.head.appendChild(style);
const nameEl=document.getElementById('heroName');
'Gadallah Mohamed'.split('').forEach((ch,i)=>{const sp=document.createElement('span');if(ch===' '){sp.className='sp';}else{sp.className='letter';sp.textContent=ch;sp.style.animation=`letterIn .5s ${.05*i+.4}s forwards cubic-bezier(.34,1.56,.64,1)`;}nameEl.appendChild(sp);});

setTimeout(()=>{document.getElementById('heroRole').textContent='Flutter Specialist · Mobile Developer · IoT Engineer';},900);

const lines=[
  {t:'<span class="kw">class </span><span class="cls">GadallahMohamed </span><span class="kw">extends </span><span class="cls">FlutterDeveloper</span> {',d:200},
  {t:'&nbsp;&nbsp;<span class="kw">final </span><span class="cls">String </span><span class="prop">location&nbsp;&nbsp;</span> = <span class="str">\'Beheira, Egypt\'</span>;',d:550},
  {t:'&nbsp;&nbsp;<span class="kw">final </span><span class="cls">String </span><span class="prop">university</span> = <span class="str">\'New Assiut Technological University\'</span>;',d:900},
  {t:'&nbsp;&nbsp;<span class="kw">final </span><span class="cls">String </span><span class="prop">status&nbsp;&nbsp;&nbsp;&nbsp;</span> = <span class="str">\'Open for remote opportunities\'</span>;',d:1250},
  {t:'',d:1500},
  {t:'&nbsp;&nbsp;<span class="cls">List</span>&lt;<span class="cls">String</span>&gt; <span class="kw">get </span><span class="fn">currentFocus</span> => [',d:1700},
  {t:'&nbsp;&nbsp;&nbsp;&nbsp;<span class="str">\'📱 Cross-platform apps — Flutter & Dart\'</span>,',d:2000},
  {t:'&nbsp;&nbsp;&nbsp;&nbsp;<span class="str">\'🤖 AI & Computer Vision in mobile\'</span>,',d:2280},
  {t:'&nbsp;&nbsp;&nbsp;&nbsp;<span class="str">\'⚙️  IoT & Robotics control systems\'</span>,',d:2560},
  {t:'&nbsp;&nbsp;&nbsp;&nbsp;<span class="str">\'🏆 Competitive Programming (ICPC)\'</span>,',d:2840},
  {t:'&nbsp;&nbsp;];',d:3100},
  {t:'}',d:3300},
];
const cb=document.getElementById('codeBody');cb.innerHTML='';let ln=1;
lines.forEach(({t,d})=>{setTimeout(()=>{const div=document.createElement('div');div.style.cssText='opacity:0;transform:translateX(-8px);transition:all .28s';const lnEl=document.createElement('span');lnEl.className='ln';lnEl.textContent=String(ln++).padStart(2,' ');div.appendChild(lnEl);const c=document.createElement('span');c.innerHTML=t||'&nbsp;';div.appendChild(c);cb.appendChild(div);requestAnimationFrame(()=>requestAnimationFrame(()=>{div.style.opacity='1';div.style.transform='translateX(0)';}));},d+1500);});

const phrases=['Building cross-platform apps with Flutter','Crafting IoT & Robotics systems','Integrating AI into mobile experiences','Clean Architecture enthusiast','ICPC Competitive Programmer'];
let pi=0,ci=0,del=false,txt='';const tel=document.getElementById('typingText');
function type(){const p=phrases[pi];if(!del){txt=p.slice(0,++ci);if(ci===p.length){del=true;setTimeout(type,1800);return;}}else{txt=p.slice(0,--ci);if(ci===0){del=false;pi=(pi+1)%phrases.length;}}tel.textContent=txt;setTimeout(type,del?35:60);}
setTimeout(type,1400);

const obs=new IntersectionObserver(e=>e.forEach(x=>{if(x.isIntersecting)x.target.classList.add('visible');}),{threshold:.1});
document.querySelectorAll('[data-sec]').forEach(el=>obs.observe(el));

function countUp(id,target,sfx){const el=document.getElementById(id);if(!el)return;let n=0;const s=target/60;const t=setInterval(()=>{n=Math.min(n+s,target);el.textContent=Math.floor(n)+sfx;if(n>=target)clearInterval(t);},16);}
setTimeout(()=>{countUp('s1',6,'+');countUp('s2',3,'+');},800);

const stBtn=document.getElementById('stBtn');
window.addEventListener('scroll',()=>stBtn.classList.toggle('show',window.scrollY>400));

const readme=`<div align="center">

\`\`\`
╔══════════════════════════════════════════════════╗
║      Gadallah Mohamed  //  Flutter Developer     ║
║      Mobile · IoT · Clean Architecture · ICPC   ║
╚══════════════════════════════════════════════════╝
\`\`\`

[![LinkedIn](https://img.shields.io/badge/LinkedIn-%230077B5.svg?style=flat-square&logo=linkedin&logoColor=white)](https://linkedin.com/in/gadallah-mohamed)
[![Gmail](https://img.shields.io/badge/Gmail-D14836?style=flat-square&logo=gmail&logoColor=white)](mailto:goodashalaa912@gmail.com)
[![GitHub](https://img.shields.io/badge/GitHub-%23121011.svg?style=flat-square&logo=github&logoColor=white)](https://github.com/GadallahMohamed41)
![Profile Views](https://komarev.com/ghpvc/?username=GadallahMohamed41&style=flat-square&color=brightgreen)

</div>

---

\`\`\`dart
class GadallahMohamed extends FlutterDeveloper {
  final String location   = 'Beheira, Egypt';
  final String degree     = 'B.Sc. IT — New Assiut Technological University (2026)';
  final String status     = 'Open for remote opportunities';

  List<String> get currentFocus => [
    '📱  Cross-platform apps — Flutter & Dart',
    '🤖  AI & Computer Vision in mobile',
    '⚙️   IoT & Robotics control systems',
    '🏆  Competitive Programming (ICPC)',
  ];
}
\`\`\`

---

## 🛠 Tech Stack

| Category | Technologies |
|---|---|
| **Mobile** | Flutter · Dart · Android |
| **Architecture** | Clean Architecture · MVVM · MVC |
| **State Management** | BLoC · Provider |
| **Backend & Cloud** | Firebase (Auth · Firestore · FCM) · REST API · SQLite |
| **AI & IoT** | OpenCV · Arduino · Bluetooth (HC-05) · Wi-Fi |
| **Languages** | C++ · Java · Python · Assembly |
| **Tools** | Git · GitHub · VS Code · Android Studio |

---

## 🚀 Projects

### 🦾 Robotic Arm Control System \`2026\`
Flutter IoT system for real-time wireless control of a physical robotic arm — Mobile & Desktop.
- Bluetooth (HC-05) and Wi-Fi dual connectivity
- Movement recording, playback, import/export sequences
- Emergency stop & full joint control · Arduino UNO + servo motors

\`Flutter\` \`Arduino\` \`Bluetooth\` \`Wi-Fi\` \`IoT\`

---

### ✈️ Travel & Booking App \`2025\`
Full-featured travel app — smart search, wishlist, multiple payments, dark mode · Clean Architecture.

\`Flutter\` \`BLoC\` \`REST API\` \`Clean Architecture\`

---

### 🔒 Smart Security App \`2024\`
Real-time alerts and remote control for IoT-based home security · Firebase push notifications.

\`Flutter\` \`Firebase\` \`IoT\` \`FCM\`

---

### 🏦 Banking App \`2023\`
Secure Flutter banking app with SQLite and transactional balance transfers.

\`Flutter\` \`SQLite\` \`Dart\`

---

## 💼 Experience

**Flutter Teaching Assistant — TechUP Academy** \`Dec 2025 – Present\`
- Delivered Flutter & Dart sessions alongside senior instructors
- Debugged live code and guided students through hands-on projects
- Simplified complex concepts and reviewed assignments with structured feedback

---

## 🏅 Awards & Certifications

- 🥇 **Top 3 Achiever** — GAIC Program *(EU-funded · National Council for Women)*
- 📜 **Mobile App Development Diploma** — ITI
- 📜 **SprintUp — Mobile Development by Flutter** — Sprints
- 📜 **Flutter Program (60 hrs)** — Creativa Innovation Hub · ITIDA · TIEC · MOR

---

## 📊 GitHub Stats

<div align="center">

![Stats](https://github-readme-stats.vercel.app/api?username=GadallahMohamed41&show_icons=true&theme=github_dark&hide_border=true&count_private=true&bg_color=0d1117)

![Streak](https://github-readme-streak-stats.herokuapp.com?user=GadallahMohamed41&theme=github-dark-blue&hide_border=true&background=0d1117)

![Languages](https://github-readme-stats.vercel.app/api/top-langs/?username=GadallahMohamed41&layout=compact&theme=github_dark&hide_border=true&bg_color=0d1117)

</div>

---

<div align="center">

🇸🇦 Arabic (Native) · 🇬🇧 English B2 · 🌐 Open for Remote Work

\`// "Building apps that matter, one widget at a time."\`

</div>`;

function copyReadme(){
  navigator.clipboard.writeText(readme).then(()=>{
    const t=document.getElementById('toast');t.classList.add('show');setTimeout(()=>t.classList.remove('show'),2500);
    const btn=document.getElementById('copyBtn');btn.innerHTML='✅ Copied!';
    setTimeout(()=>{btn.innerHTML='<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><rect x="9" y="9" width="13" height="13" rx="2"/><path d="M5 15H4a2 2 0 01-2-2V4a2 2 0 012-2h9a2 2 0 012 2v1"/></svg> Copy README for GitHub';},2400);
  });
}
</script>
</body>
</html>
