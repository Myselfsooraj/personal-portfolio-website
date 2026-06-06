<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Suraj Bhardwaj — Cybersecurity</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500&family=Syne:wght@400;500;600;700;800&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<style>
/* ─── RESET ─── */
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
html{font-size:16px;scroll-behavior:smooth}
body{background:#070707;color:#e8e8e2;font-family:'Inter',sans-serif;font-weight:300;line-height:1.6;overflow-x:hidden;cursor:none}
img,video{max-width:100%;display:block}
a{text-decoration:none;color:inherit}
::selection{background:rgba(0,255,170,.15);color:#fff}
::-webkit-scrollbar{width:2px}::-webkit-scrollbar-track{background:#070707}::-webkit-scrollbar-thumb{background:#333}

/* ─── CUSTOM CURSOR ─── */
#cursor-ring{position:fixed;top:0;left:0;width:36px;height:36px;border:1px solid rgba(255,255,255,.3);border-radius:50%;pointer-events:none;z-index:99999;transform:translate(-50%,-50%);transition:transform .08s,width .25s,height .25s,border-color .25s,background .25s}
#cursor-dot{position:fixed;top:0;left:0;width:5px;height:5px;background:#fff;border-radius:50%;pointer-events:none;z-index:99999;transform:translate(-50%,-50%);transition:transform .04s}
body.hover-active #cursor-ring{width:60px;height:60px;border-color:rgba(0,255,170,.5);background:rgba(0,255,170,.04)}
body.link-active #cursor-ring{width:80px;height:80px;border-color:rgba(0,255,170,.7);background:rgba(0,255,170,.07)}

/* ─── NOISE GRAIN ─── */
body::before{content:'';position:fixed;inset:0;z-index:1;opacity:.032;pointer-events:none;
  background-image:url("data:image/svg+xml,%3Csvg viewBox='0 0 512 512' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.75' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
  background-size:200px}

/* ─── NAV ─── */
nav{position:fixed;top:0;left:0;right:0;z-index:1000;padding:1.5rem 3rem;display:flex;align-items:center;justify-content:space-between;mix-blend-mode:normal}
.nav-logo{font-family:'Syne',sans-serif;font-weight:700;font-size:1rem;letter-spacing:.05em;color:#fff;text-transform:uppercase}
.nav-links{display:flex;gap:2.5rem;list-style:none}
.nav-links a{font-size:.75rem;letter-spacing:.12em;text-transform:uppercase;color:rgba(255,255,255,.4);transition:color .25s}
.nav-links a:hover{color:#fff}
.nav-right{display:flex;align-items:center;gap:1.5rem}
.nav-status{display:flex;align-items:center;gap:.5rem;font-size:.7rem;letter-spacing:.1em;color:rgba(255,255,255,.35);text-transform:uppercase}
.status-blink{width:5px;height:5px;background:#00ffaa;border-radius:50%;animation:sblink 2s ease-in-out infinite}
@keyframes sblink{0%,100%{opacity:1;box-shadow:0 0 0 0 rgba(0,255,170,.5)}70%{opacity:.6;box-shadow:0 0 0 5px rgba(0,255,170,0)}}

/* ─── HERO ─── */
#hero{min-height:100vh;display:flex;flex-direction:column;justify-content:flex-end;padding:0 3rem 4rem;position:relative;overflow:hidden}
.hero-bg{position:absolute;inset:0;z-index:0}
#hero-canvas{width:100%;height:100%;display:block;opacity:.6}
.hero-content{position:relative;z-index:2}
.hero-top-tag{font-size:.72rem;letter-spacing:.18em;text-transform:uppercase;color:rgba(255,255,255,.35);margin-bottom:2rem;display:flex;align-items:center;gap:.75rem}
.hero-top-tag::before{content:'';display:block;width:24px;height:1px;background:rgba(255,255,255,.25)}
.hero-name{font-family:'Syne',sans-serif;font-weight:800;font-size:clamp(3.5rem,10vw,10rem);line-height:.92;letter-spacing:-.03em;color:#fff;margin-bottom:1.5rem;overflow:hidden}
.hero-name .line{display:block;overflow:hidden}
.hero-name .line span{display:inline-block;transform:translateY(110%);animation:lineUp .9s cubic-bezier(.16,1,.3,1) forwards}
.hero-name .line:nth-child(2) span{animation-delay:.1s}
@keyframes lineUp{to{transform:translateY(0)}}
.hero-bottom{display:flex;align-items:flex-end;justify-content:space-between;gap:2rem;flex-wrap:wrap}
.hero-desc{font-size:clamp(.85rem,1.2vw,1rem);color:rgba(255,255,255,.45);max-width:360px;line-height:1.8;font-weight:300}
.hero-desc em{color:rgba(0,255,170,.75);font-style:normal}
.hero-meta{text-align:right}
.hero-role{font-family:'Syne',sans-serif;font-size:.8rem;font-weight:500;letter-spacing:.15em;text-transform:uppercase;color:rgba(255,255,255,.3);margin-bottom:.4rem}
.hero-loc{font-size:.72rem;color:rgba(255,255,255,.2);letter-spacing:.1em}
.hero-scroll{position:absolute;bottom:2.5rem;left:50%;transform:translateX(-50%);display:flex;flex-direction:column;align-items:center;gap:.5rem;z-index:2}
.scroll-line{width:1px;height:50px;background:linear-gradient(to bottom,rgba(255,255,255,.3),transparent);animation:scrollAnim 2s ease-in-out infinite}
@keyframes scrollAnim{0%,100%{transform:scaleY(1);opacity:.5}50%{transform:scaleY(1.3);opacity:1}}
.scroll-label{font-size:.6rem;letter-spacing:.2em;color:rgba(255,255,255,.2);text-transform:uppercase;transform:rotate(90deg);white-space:nowrap}

/* ─── MARQUEE ─── */
.marquee-section{padding:1.5rem 0;border-top:1px solid rgba(255,255,255,.06);border-bottom:1px solid rgba(255,255,255,.06);overflow:hidden;position:relative;z-index:10}
.marquee-track{display:flex;gap:0;animation:marquee 22s linear infinite;width:max-content}
.marquee-item{font-family:'Syne',sans-serif;font-size:clamp(.85rem,1.5vw,1.1rem);font-weight:600;letter-spacing:.08em;text-transform:uppercase;color:rgba(255,255,255,.12);padding:0 2.5rem;white-space:nowrap;display:flex;align-items:center;gap:2.5rem}
.marquee-item::after{content:'✦';font-size:.5rem;color:rgba(0,255,170,.4)}
@keyframes marquee{0%{transform:translateX(0)}100%{transform:translateX(-50%)}}

/* ─── SECTIONS ─── */
section{position:relative;z-index:10}
.container{padding:7rem 3rem}
.section-eyebrow{font-size:.68rem;letter-spacing:.2em;text-transform:uppercase;color:rgba(0,255,170,.6);margin-bottom:1.25rem;display:flex;align-items:center;gap:.75rem}
.section-eyebrow::before{content:'';display:block;width:20px;height:1px;background:rgba(0,255,170,.4)}
.section-title{font-family:'Syne',sans-serif;font-weight:800;font-size:clamp(2.2rem,5vw,5rem);line-height:.95;letter-spacing:-.03em;color:#fff;margin-bottom:3.5rem}

/* ─── ABOUT ─── */
#about{background:#070707}
.about-grid{display:grid;grid-template-columns:1fr 1fr;gap:5rem;align-items:start}
.about-text{font-size:1rem;color:rgba(255,255,255,.5);line-height:1.9}
.about-text p{margin-bottom:1.25rem}
.about-text strong{color:#fff;font-weight:400}
.about-text em{color:rgba(0,255,170,.8);font-style:normal}
.about-right{}
.id-block{border:1px solid rgba(255,255,255,.06);padding:2rem;background:#0d0d0d;position:relative;overflow:hidden}
.id-block::before{content:'';position:absolute;top:0;left:0;right:0;height:1px;background:linear-gradient(90deg,transparent,rgba(0,255,170,.3),transparent)}
.id-tag{position:absolute;top:1.25rem;right:1.25rem;font-size:.6rem;letter-spacing:.15em;text-transform:uppercase;color:rgba(0,255,170,.5);border:1px solid rgba(0,255,170,.2);padding:.25rem .65rem}
.id-avatar{width:56px;height:56px;background:rgba(0,255,170,.06);border:1px solid rgba(0,255,170,.15);display:flex;align-items:center;justify-content:center;font-family:'Syne',sans-serif;font-weight:800;font-size:1.1rem;color:rgba(0,255,170,.7);margin-bottom:1.5rem}
.id-name{font-family:'Syne',sans-serif;font-weight:700;font-size:1.1rem;color:#fff;margin-bottom:.2rem}
.id-role{font-size:.72rem;color:rgba(255,255,255,.3);letter-spacing:.1em;text-transform:uppercase;margin-bottom:1.75rem}
.id-rows{display:flex;flex-direction:column;gap:0;border-top:1px solid rgba(255,255,255,.06)}
.id-row{display:flex;gap:1.25rem;padding:.75rem 0;border-bottom:1px solid rgba(255,255,255,.04);font-size:.8rem;align-items:flex-start}
.id-k{color:rgba(255,255,255,.25);width:70px;flex-shrink:0;letter-spacing:.08em;text-transform:uppercase;font-size:.65rem;margin-top:.1rem}
.id-v{color:rgba(255,255,255,.65)}
.id-v a{color:rgba(0,255,170,.7);transition:color .2s}
.id-v a:hover{color:#00ffaa}
.available-pill{display:inline-flex;align-items:center;gap:.4rem;background:rgba(0,255,170,.06);border:1px solid rgba(0,255,170,.18);color:rgba(0,255,170,.7);font-size:.65rem;letter-spacing:.12em;text-transform:uppercase;padding:.3rem .75rem;margin-top:.5rem}
/* stat row */
.stat-strip{display:grid;grid-template-columns:repeat(3,1fr);gap:0;margin-top:3rem;border:1px solid rgba(255,255,255,.06)}
.stat-item{padding:1.5rem;text-align:center;border-right:1px solid rgba(255,255,255,.06)}
.stat-item:last-child{border-right:none}
.stat-num{font-family:'Syne',sans-serif;font-weight:800;font-size:2.5rem;color:#fff;line-height:1;margin-bottom:.35rem}
.stat-label{font-size:.65rem;letter-spacing:.12em;text-transform:uppercase;color:rgba(255,255,255,.25)}

/* ─── SKILLS ─── */
#skills{background:#0a0a0a}
.skills-wrap{display:grid;grid-template-columns:1fr 1fr;gap:5rem;align-items:start}
.skills-list{display:flex;flex-direction:column;gap:0}
.skill-item{display:flex;align-items:center;gap:2rem;padding:1.5rem 0;border-bottom:1px solid rgba(255,255,255,.05);position:relative;overflow:hidden;transition:padding-left .3s}
.skill-item:first-child{border-top:1px solid rgba(255,255,255,.05)}
.skill-item:hover{padding-left:.75rem}
.skill-num{font-family:'Syne',sans-serif;font-size:.7rem;color:rgba(255,255,255,.18);width:28px;flex-shrink:0}
.skill-name{font-family:'Syne',sans-serif;font-size:1rem;font-weight:600;color:#fff;flex:1;letter-spacing:-.01em}
.skill-level{font-size:.65rem;letter-spacing:.12em;text-transform:uppercase;color:rgba(255,255,255,.25);width:90px;text-align:right;flex-shrink:0}
.skill-bar-wrap{width:80px;flex-shrink:0}
.skill-bar-bg{height:1px;background:rgba(255,255,255,.08)}
.skill-bar-fill{height:1px;background:#00ffaa;width:0;transition:width 1.4s cubic-bezier(.16,1,.3,1)}
/* right side — cyber tags cloud */
.skills-right{display:flex;flex-direction:column;gap:2rem}
.skill-category{border:1px solid rgba(255,255,255,.05);padding:1.5rem;background:#0d0d0d;position:relative}
.sc-label{font-size:.65rem;letter-spacing:.15em;text-transform:uppercase;color:rgba(0,255,170,.5);margin-bottom:1rem}
.sc-tags{display:flex;flex-wrap:wrap;gap:.5rem}
.sc-tag{font-size:.72rem;padding:.35rem .8rem;border:1px solid rgba(255,255,255,.08);color:rgba(255,255,255,.4);transition:all .2s;letter-spacing:.04em}
.sc-tag:hover,.sc-tag.active{border-color:rgba(0,255,170,.3);color:rgba(0,255,170,.8);background:rgba(0,255,170,.04)}
.sc-tag.learning{border-color:rgba(255,60,100,.25);color:rgba(255,60,100,.6)}

/* ─── WORK ─── */
#experience{background:#070707}
.exp-item{display:grid;grid-template-columns:180px 1fr;gap:4rem;padding:3.5rem 0;border-bottom:1px solid rgba(255,255,255,.05);position:relative}
.exp-item:first-child{border-top:1px solid rgba(255,255,255,.05)}
.exp-left{}
.exp-company{font-family:'Syne',sans-serif;font-size:.75rem;font-weight:600;letter-spacing:.1em;text-transform:uppercase;color:rgba(255,255,255,.3);margin-bottom:.35rem}
.exp-period{font-size:.68rem;color:rgba(255,255,255,.2);letter-spacing:.06em;margin-bottom:.25rem}
.exp-loc{font-size:.65rem;color:rgba(255,255,255,.15);letter-spacing:.04em}
.exp-right{}
.exp-role{font-family:'Syne',sans-serif;font-size:clamp(1.4rem,2.5vw,2.2rem);font-weight:700;color:#fff;letter-spacing:-.02em;margin-bottom:1.5rem;line-height:1.1}
.exp-bullets{list-style:none;display:flex;flex-direction:column;gap:.6rem;margin-bottom:1.5rem}
.exp-bullets li{font-size:.85rem;color:rgba(255,255,255,.45);padding-left:1rem;position:relative;line-height:1.7}
.exp-bullets li::before{content:'—';position:absolute;left:0;color:rgba(0,255,170,.4);font-size:.75rem}
.exp-stack{display:flex;flex-wrap:wrap;gap:.4rem}
.exp-tag{font-size:.65rem;padding:.25rem .65rem;border:1px solid rgba(255,255,255,.08);color:rgba(255,255,255,.3);letter-spacing:.06em}

/* ─── EDUCATION ─── */
#education{background:#0a0a0a}
.edu-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:1px;background:rgba(255,255,255,.05)}
.edu-card{background:#0a0a0a;padding:2.5rem;position:relative;overflow:hidden;transition:background .3s}
.edu-card:hover{background:#0f0f0f}
.edu-card.featured::after{content:'';position:absolute;top:0;left:0;right:0;height:1px;background:linear-gradient(90deg,transparent,rgba(0,255,170,.5),transparent)}
.edu-yr{font-size:.68rem;letter-spacing:.1em;color:rgba(255,255,255,.2);margin-bottom:.75rem;text-transform:uppercase}
.edu-deg{font-family:'Syne',sans-serif;font-size:1rem;font-weight:600;color:#fff;line-height:1.3;margin-bottom:.35rem}
.edu-school{font-size:.75rem;color:rgba(0,255,170,.4);letter-spacing:.04em;margin-bottom:.75rem}
.edu-score{font-family:'Syne',sans-serif;font-size:2rem;font-weight:800;color:rgba(255,255,255,.12)}
.edu-badge{display:inline-block;font-size:.58rem;letter-spacing:.15em;padding:.2rem .6rem;border:1px solid rgba(0,255,170,.2);color:rgba(0,255,170,.5);text-transform:uppercase;margin-top:.5rem}

/* ─── CERTS ─── */
#certs{background:#070707}
.certs-grid{display:grid;grid-template-columns:1fr 1fr;gap:5rem}
.certs-left{}
.cert-item{display:flex;gap:1.25rem;padding:1.5rem 0;border-bottom:1px solid rgba(255,255,255,.05);align-items:flex-start}
.cert-item:first-child{border-top:1px solid rgba(255,255,255,.05)}
.cert-num{font-family:'Syne',sans-serif;font-size:.65rem;color:rgba(255,255,255,.15);width:24px;flex-shrink:0;padding-top:.15rem}
.cert-content{}
.cert-name{font-size:.9rem;color:#fff;font-weight:400;margin-bottom:.25rem;line-height:1.4}
.cert-by{font-size:.7rem;color:rgba(255,255,255,.25);letter-spacing:.06em}
.target-block{margin-top:2.5rem;padding:1.5rem;border:1px solid rgba(255,255,255,.05);background:#0d0d0d}
.target-label{font-size:.65rem;letter-spacing:.15em;text-transform:uppercase;color:rgba(255,100,80,.5);margin-bottom:1rem;display:flex;align-items:center;gap:.6rem}
.target-label::before{content:'▸';color:rgba(255,100,80,.5)}
.target-item{font-size:.8rem;color:rgba(255,255,255,.35);padding:.45rem 0;border-bottom:1px solid rgba(255,255,255,.04);display:flex;align-items:center;gap:.75rem;transition:color .2s}
.target-item:last-child{border:none}
.target-item:hover{color:rgba(255,255,255,.6)}
.target-item::before{content:'→';color:rgba(0,255,170,.35);font-size:.75rem}
.awards-block{}
.award-row{padding:1.5rem 0;border-bottom:1px solid rgba(255,255,255,.05);transition:padding-left .25s;cursor:default}
.award-row:first-child{border-top:1px solid rgba(255,255,255,.05)}
.award-row:hover{padding-left:.75rem}
.award-idx{font-size:.65rem;color:rgba(255,255,255,.18);letter-spacing:.08em;margin-bottom:.4rem}
.award-title{font-family:'Syne',sans-serif;font-size:.95rem;font-weight:600;color:#fff;margin-bottom:.3rem;line-height:1.3}
.award-desc{font-size:.78rem;color:rgba(255,255,255,.3);line-height:1.6}

/* ─── TERMINAL ─── */
#terminal-section{background:#0a0a0a}
.term-outer{border:1px solid rgba(255,255,255,.07);background:#0d0d0d;max-width:860px}
.term-bar{display:flex;align-items:center;gap:.6rem;padding:.65rem 1rem;background:#111;border-bottom:1px solid rgba(255,255,255,.06)}
.tdot{width:10px;height:10px;border-radius:50%}
.tdot.r{background:#ff5f56}.tdot.y{background:#ffbd2e}.tdot.g{background:#27c93f}
.term-title-bar{font-size:.65rem;color:rgba(255,255,255,.2);letter-spacing:.08em;margin-left:.5rem;flex:1}
.term-enc{font-size:.6rem;color:rgba(0,255,170,.4);letter-spacing:.1em}
.term-body{padding:1.25rem;min-height:300px;max-height:380px;overflow-y:auto;font-size:.78rem;font-family:'SF Mono','Fira Mono','Consolas',monospace}
.term-body::-webkit-scrollbar{width:2px}.term-body::-webkit-scrollbar-thumb{background:#333}
.tl{line-height:1.6;margin-bottom:.1rem}
.tl .tp{color:rgba(0,255,170,.7)}.tl .tc{color:#fff}.tl .to{color:rgba(255,255,255,.4)}
.tl .tok{color:#00ff88}.tl .ter{color:#ff4d6a}.tl .tww{color:#ffcc44}.tl .tii{color:#60aaff}
.term-input-wrap{display:flex;align-items:center;gap:.75rem;padding:.65rem 1.25rem;border-top:1px solid rgba(255,255,255,.06)}
.term-ps1{font-size:.78rem;color:rgba(0,255,170,.7);font-family:'SF Mono','Fira Mono',monospace;white-space:nowrap}
#TI{flex:1;background:transparent;border:none;outline:none;font-family:'SF Mono','Fira Mono',monospace;font-size:.78rem;color:#fff;caret-color:rgba(0,255,170,.8)}

/* ─── GOAL ─── */
#goal{background:#0d0d0d;text-align:center}
.goal-hl{font-family:'Syne',sans-serif;font-size:clamp(1.5rem,3vw,3rem);font-weight:800;color:#fff;max-width:700px;margin:0 auto 3.5rem;line-height:1.15;letter-spacing:-.03em}
.goal-hl em{color:rgba(0,255,170,.8);font-style:normal}
.goal-hl strong{color:rgba(255,80,100,.8)}
.roadmap{max-width:720px;margin:0 auto;display:flex;flex-direction:column;gap:0}
.rm{display:flex;align-items:flex-start;gap:1.5rem;padding:1.25rem 1.5rem;border:1px solid rgba(255,255,255,.05);background:#0a0a0a;margin-bottom:1px;transition:background .25s}
.rm:hover{background:#0f0f0f}
.rm-badge{flex-shrink:0;font-size:.6rem;letter-spacing:.1em;padding:.25rem .6rem;border:1px solid;text-transform:uppercase;white-space:nowrap;margin-top:.1rem}
.rm-badge.a{border-color:rgba(0,255,170,.3);color:rgba(0,255,170,.6)}
.rm-badge.n{border-color:rgba(255,200,50,.3);color:rgba(255,200,50,.6)}
.rm-badge.p{border-color:rgba(255,255,255,.12);color:rgba(255,255,255,.25)}
.rm-body{}
.rm-title{font-family:'Syne',sans-serif;font-size:.9rem;font-weight:600;color:#fff;margin-bottom:.2rem}
.rm-desc{font-size:.75rem;color:rgba(255,255,255,.3);line-height:1.6}

/* ─── CONTACT ─── */
#contact{background:#070707}
.contact-wrap{display:grid;grid-template-columns:1fr 1fr;gap:6rem;align-items:start}
.contact-links{display:flex;flex-direction:column;gap:0}
.cc-link{display:flex;align-items:center;gap:1.25rem;padding:1.25rem 0;border-bottom:1px solid rgba(255,255,255,.05);text-decoration:none;transition:padding-left .3s}
.cc-link:first-child{border-top:1px solid rgba(255,255,255,.05)}
.cc-link:hover{padding-left:.75rem}
.cc-icon{width:36px;height:36px;border:1px solid rgba(255,255,255,.08);display:flex;align-items:center;justify-content:center;font-size:.75rem;font-family:'Syne',sans-serif;font-weight:700;color:rgba(255,255,255,.3);flex-shrink:0;transition:border-color .2s,color .2s}
.cc-link:hover .cc-icon{border-color:rgba(0,255,170,.3);color:rgba(0,255,170,.7)}
.cc-info{}
.cc-label{font-size:.6rem;letter-spacing:.12em;text-transform:uppercase;color:rgba(255,255,255,.2);margin-bottom:.15rem}
.cc-value{font-size:.85rem;color:rgba(255,255,255,.55)}
.cc-arr{margin-left:auto;color:rgba(255,255,255,.15);font-size:1rem;transition:transform .25s,color .25s}
.cc-link:hover .cc-arr{transform:translate(4px,-4px);color:rgba(0,255,170,.6)}
.contact-right{}
.contact-note{font-size:.9rem;color:rgba(255,255,255,.4);line-height:1.9;margin-bottom:2rem}
.contact-note strong{color:#fff;font-weight:400}
.contact-note em{color:rgba(0,255,170,.7);font-style:normal}

/* ─── FOOTER ─── */
footer{padding:2rem 3rem;border-top:1px solid rgba(255,255,255,.05);display:flex;justify-content:space-between;align-items:center;position:relative;z-index:10}
.footer-copy{font-size:.68rem;color:rgba(255,255,255,.2);letter-spacing:.06em}
.footer-tag{font-size:.68rem;color:rgba(0,255,170,.3);letter-spacing:.1em;text-transform:uppercase}

/* ─── FADE IN ─── */
.reveal{opacity:0;transform:translateY(32px);transition:opacity .8s cubic-bezier(.16,1,.3,1),transform .8s cubic-bezier(.16,1,.3,1)}
.reveal.in{opacity:1;transform:none}
.reveal-left{opacity:0;transform:translateX(-32px);transition:opacity .8s cubic-bezier(.16,1,.3,1),transform .8s cubic-bezier(.16,1,.3,1)}
.reveal-left.in{opacity:1;transform:none}
.reveal-right{opacity:0;transform:translateX(32px);transition:opacity .8s cubic-bezier(.16,1,.3,1),transform .8s cubic-bezier(.16,1,.3,1)}
.reveal-right.in{opacity:1;transform:none}

@media(max-width:900px){
  nav{padding:1.25rem 1.5rem}
  .nav-links{gap:1.25rem}
  .container{padding:5rem 1.5rem}
  #hero{padding:0 1.5rem 3.5rem}
  .about-grid,.skills-wrap,.exp-item,.edu-grid,.certs-grid,.contact-wrap{grid-template-columns:1fr;gap:3rem}
  footer{padding:1.5rem;flex-direction:column;gap:.75rem;text-align:center}
  .hero-bottom{flex-direction:column;align-items:flex-start;gap:1rem}
  .hero-meta{text-align:left}
}

/* ─── 3D HERO SCENE ─── */
#three-hero{position:absolute;inset:0;z-index:1;pointer-events:none}
#three-hero canvas{width:100%!important;height:100%!important}

/* ─── 3D GLOBE SECTION ─── */
#globe-section{position:relative;z-index:10;overflow:hidden;background:#070707;border-top:1px solid rgba(255,255,255,.06);border-bottom:1px solid rgba(255,255,255,.06)}
.globe-inner{display:grid;grid-template-columns:1fr 480px;align-items:center;gap:0;min-height:600px}
.globe-text{padding:6rem 3rem 6rem 5rem}
.globe-canvas-wrap{height:600px;position:relative}
#three-globe{width:100%;height:100%}
#three-globe canvas{width:100%!important;height:100%!important}

/* ─── 3D LOCK SECTION ─── */
#lock-scene-wrap{position:relative;height:420px;overflow:hidden;background:#0a0a0a;border-top:1px solid rgba(255,255,255,.06)}
#three-lock{position:absolute;inset:0}
#three-lock canvas{width:100%!important;height:100%!important}
.lock-overlay{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;pointer-events:none;z-index:2}
.lock-text-center{text-align:center}
.lock-tagline{font-family:'Syne',sans-serif;font-weight:800;font-size:clamp(1.8rem,4vw,4rem);color:#fff;letter-spacing:-.03em;line-height:1.05;margin-bottom:1rem}
.lock-tagline em{color:rgba(0,255,170,.8);font-style:normal}
.lock-sub{font-size:.8rem;color:rgba(255,255,255,.3);letter-spacing:.15em;text-transform:uppercase}

@media(max-width:900px){
  .globe-inner{grid-template-columns:1fr}
  .globe-canvas-wrap{height:320px}
  .globe-text{padding:4rem 1.5rem 3rem}
  #lock-scene-wrap{height:320px}
}

</style>
</head>
<body>

<!-- CURSOR -->
<div id="cursor-ring"></div>
<div id="cursor-dot"></div>

<!-- NAV -->
<nav id="NAV" style="opacity:0;transition:opacity .6s .8s">
  <a href="#hero" class="nav-logo">Suraj.sys</a>
  <ul class="nav-links">
    <li><a href="#about">About</a></li>
    <li><a href="#skills">Skills</a></li>
    <li><a href="#experience">Work</a></li>
    <li><a href="#education">Education</a></li>
    <li><a href="#terminal-section">Terminal</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
  <div class="nav-right">
    <div class="nav-status"><div class="status-blink"></div>System online</div>
    <span id="NAV-CLK" style="font-size:.7rem;color:rgba(255,255,255,.2);letter-spacing:.06em;font-family:'SF Mono','Fira Mono',monospace"></span>
  </div>
</nav>

<!-- ══ HERO ══ -->
<section id="hero">
  <div class="hero-bg"><canvas id="hero-canvas"></canvas></div>
  <div id="three-hero"></div>
  <div class="hero-content">
    <div class="hero-top-tag">Cybersecurity Portfolio — 2025</div>
    <div class="hero-name">
      <div class="line"><span>Suraj</span></div>
      <div class="line"><span>Bhardwaj</span></div>
    </div>
    <div class="hero-bottom">
      <p class="hero-desc">Frontend developer building toward <em>ethical hacking</em> and <em>security engineering</em> — Haryana, India.</p>
      <div class="hero-meta">
        <div class="hero-role">Frontend Dev → Cyber Engineer</div>
        <div class="hero-loc">Yamunanagar · Haryana · IN</div>
      </div>
    </div>
  </div>
  <div class="hero-scroll"><div class="scroll-line"></div><span class="scroll-label">Scroll</span></div>
</section>

<!-- MARQUEE -->
<div class="marquee-section">
  <div class="marquee-track" id="marquee">
    <div class="marquee-item">Frontend Development</div>
    <div class="marquee-item">Cybersecurity</div>
    <div class="marquee-item">Ethical Hacking</div>
    <div class="marquee-item">Network Security</div>
    <div class="marquee-item">HTML · CSS · JS</div>
    <div class="marquee-item">C / C++</div>
    <div class="marquee-item">SQL · Oracle DB</div>
    <div class="marquee-item">Git · GitHub</div>
    <div class="marquee-item">BCA Student</div>
    <div class="marquee-item">Open to Work</div>
    <div class="marquee-item">Frontend Development</div>
    <div class="marquee-item">Cybersecurity</div>
    <div class="marquee-item">Ethical Hacking</div>
    <div class="marquee-item">Network Security</div>
    <div class="marquee-item">HTML · CSS · JS</div>
    <div class="marquee-item">C / C++</div>
    <div class="marquee-item">SQL · Oracle DB</div>
    <div class="marquee-item">Git · GitHub</div>
    <div class="marquee-item">BCA Student</div>
    <div class="marquee-item">Open to Work</div>
  </div>
</div>

<!-- ══ 3D GLOBE SECTION ══ -->
<section id="globe-section">
  <div class="globe-inner">
    <div class="globe-text reveal-left">
      <div class="section-eyebrow">Live Threat Network</div>
      <h2 class="section-title" style="margin-bottom:1.5rem">Global<br>Cyber<br>Landscape</h2>
      <p style="font-size:.88rem;color:rgba(255,255,255,.4);line-height:1.9;max-width:380px">Every second, thousands of cyberattacks traverse the internet. Understanding this landscape — how threats propagate, where they originate, and how defences are structured — is the foundation of security engineering.</p>
      <div style="margin-top:2rem;display:flex;flex-direction:column;gap:.75rem">
        <div style="display:flex;align-items:center;gap:.75rem;font-size:.75rem;color:rgba(255,255,255,.3)"><span style="width:8px;height:8px;border-radius:50%;background:#00ffaa;flex-shrink:0"></span>Network nodes — secure connections</div>
        <div style="display:flex;align-items:center;gap:.75rem;font-size:.75rem;color:rgba(255,255,255,.3)"><span style="width:8px;height:8px;border-radius:50%;background:rgba(255,80,100,.8);flex-shrink:0"></span>Active threat vectors — attack arcs</div>
        <div style="display:flex;align-items:center;gap:.75rem;font-size:.75rem;color:rgba(255,255,255,.3)"><span style="width:8px;height:8px;border-radius:50%;background:rgba(255,200,60,.7);flex-shrink:0"></span>Monitored endpoints — under observation</div>
      </div>
    </div>
    <div class="globe-canvas-wrap">
      <div id="three-globe"></div>
    </div>
  </div>
</section>



<!-- ══ ABOUT ══ -->
<section id="about">
  <div class="container">
    <div class="about-grid">
      <div class="reveal-left">
        <div class="section-eyebrow">01 — Identity</div>
        <h2 class="section-title">About<br>Me</h2>
        <div class="about-text">
          <p>I'm a <strong>BCA student</strong> at Maharaja Agrasen College, Haryana — building web interfaces and chasing a future in <em>cybersecurity</em>.</p>
          <p>My internship at SkillCraft Technology gave me hands-on experience building <strong>4 full-stack web applications</strong> from scratch — responsive, cross-browser, version-controlled, and deployed.</p>
          <p>But what truly drives me is what sits beneath those apps — the protocols, attack surfaces, and defence mechanisms. I believe the best security engineers <em>build first, then break.</em></p>
          <p>Currently preparing for Linux fundamentals, networking deep-dives, and the <em>CEH / CompTIA Security+</em> track.</p>
        </div>
        <div class="stat-strip">
          <div class="stat-item"><div class="stat-num" data-count="4">0</div><div class="stat-label">Apps Shipped</div></div>
          <div class="stat-item"><div class="stat-num" data-count="2">0</div><div class="stat-label">Years Coding</div></div>
          <div class="stat-item"><div class="stat-num" data-count="1">0</div><div class="stat-label">Internship</div></div>
        </div>
      </div>
      <div class="reveal-right" style="transition-delay:.15s">
        <div class="id-block">
          <div class="id-tag">ID Card</div>
          <div class="id-avatar">SB</div>
          <div class="id-name">Suraj Bhardwaj</div>
          <div class="id-role">Frontend Dev · Security Aspirant</div>
          <div class="id-rows">
            <div class="id-row"><div class="id-k">Location</div><div class="id-v">Yamunanagar, Haryana, IN</div></div>
            <div class="id-row"><div class="id-k">Email</div><div class="id-v"><a href="mailto:surajbhardwaaj@gmail.com">surajbhardwaaj@gmail.com</a></div></div>
            <div class="id-row"><div class="id-k">Phone</div><div class="id-v">+91 83968 41522</div></div>
            <div class="id-row"><div class="id-k">Degree</div><div class="id-v">BCA — 2024 → 2027</div></div>
            <div class="id-row"><div class="id-k">Target</div><div class="id-v" style="color:rgba(255,80,100,.7)">CEH / CompTIA Sec+</div></div>
            <div class="id-row"><div class="id-k">Status</div><div class="id-v"><div class="available-pill"><div class="status-blink"></div>Open to opportunities</div></div></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- MARQUEE 2 (reversed) -->
<div class="marquee-section">
  <div class="marquee-track" style="animation-direction:reverse;animation-duration:28s">
    <div class="marquee-item">Suraj Bhardwaj</div>
    <div class="marquee-item">SkillCraft Intern</div>
    <div class="marquee-item">Web Applications</div>
    <div class="marquee-item">Secure Systems</div>
    <div class="marquee-item">Penetration Testing</div>
    <div class="marquee-item">CTF Enthusiast</div>
    <div class="marquee-item">HackTheBox</div>
    <div class="marquee-item">TryHackMe</div>
    <div class="marquee-item">Suraj Bhardwaj</div>
    <div class="marquee-item">SkillCraft Intern</div>
    <div class="marquee-item">Web Applications</div>
    <div class="marquee-item">Secure Systems</div>
    <div class="marquee-item">Penetration Testing</div>
    <div class="marquee-item">CTF Enthusiast</div>
    <div class="marquee-item">HackTheBox</div>
    <div class="marquee-item">TryHackMe</div>
  </div>
</div>

<!-- ══ SKILLS ══ -->
<section id="skills">
  <div class="container">
    <div class="skills-wrap">
      <div class="reveal-left">
        <div class="section-eyebrow">02 — Arsenal</div>
        <h2 class="section-title">Tech<br>Skills</h2>
        <div class="skills-list">
          <div class="skill-item"><div class="skill-num">01</div><div class="skill-name">HTML / CSS</div><div class="skill-bar-wrap"><div class="skill-bar-bg"><div class="skill-bar-fill" data-w="88"></div></div></div><div class="skill-level">Advanced</div></div>
          <div class="skill-item"><div class="skill-num">02</div><div class="skill-name">JavaScript</div><div class="skill-bar-wrap"><div class="skill-bar-bg"><div class="skill-bar-fill" data-w="72"></div></div></div><div class="skill-level">Intermediate</div></div>
          <div class="skill-item"><div class="skill-num">03</div><div class="skill-name">Git / GitHub</div><div class="skill-bar-wrap"><div class="skill-bar-bg"><div class="skill-bar-fill" data-w="75"></div></div></div><div class="skill-level">Proficient</div></div>
          <div class="skill-item"><div class="skill-num">04</div><div class="skill-name">C / C++</div><div class="skill-bar-wrap"><div class="skill-bar-bg"><div class="skill-bar-fill" data-w="62"></div></div></div><div class="skill-level">Intermediate</div></div>
          <div class="skill-item"><div class="skill-num">05</div><div class="skill-name">SQL / Oracle DB</div><div class="skill-bar-wrap"><div class="skill-bar-bg"><div class="skill-bar-fill" data-w="65"></div></div></div><div class="skill-level">Intermediate</div></div>
          <div class="skill-item" style="opacity:.55"><div class="skill-num">06</div><div class="skill-name">Cybersecurity</div><div class="skill-bar-wrap"><div class="skill-bar-bg"><div class="skill-bar-fill" data-w="28" style="background:rgba(255,80,100,.7)"></div></div></div><div class="skill-level" style="color:rgba(255,80,100,.5)">Learning</div></div>
        </div>
      </div>
      <div class="reveal-right" style="transition-delay:.15s">
        <div class="skills-right">
          <div class="skill-category">
            <div class="sc-label">Web Development</div>
            <div class="sc-tags">
              <span class="sc-tag active">HTML5</span><span class="sc-tag active">CSS3</span><span class="sc-tag active">JavaScript</span><span class="sc-tag">Responsive</span><span class="sc-tag">Cross-browser</span><span class="sc-tag">DOM</span>
            </div>
          </div>
          <div class="skill-category">
            <div class="sc-label">Dev Tools & Workflow</div>
            <div class="sc-tags">
              <span class="sc-tag active">Git</span><span class="sc-tag active">GitHub</span><span class="sc-tag active">VS Code</span><span class="sc-tag">Canva</span>
            </div>
          </div>
          <div class="skill-category">
            <div class="sc-label">Databases</div>
            <div class="sc-tags">
              <span class="sc-tag active">SQL</span><span class="sc-tag active">Oracle DB</span><span class="sc-tag">Suvidha ERP</span>
            </div>
          </div>
          <div class="skill-category" style="border-color:rgba(255,80,100,.1)">
            <div class="sc-label" style="color:rgba(255,80,100,.5)">Cybersecurity — In Training</div>
            <div class="sc-tags">
              <span class="sc-tag learning">Network Security</span><span class="sc-tag learning">Ethical Hacking</span><span class="sc-tag learning">Linux CLI</span><span class="sc-tag learning">OSINT</span><span class="sc-tag learning">CTF</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ══ EXPERIENCE ══ -->
<section id="experience">
  <div class="container">
    <div class="reveal">
      <div class="section-eyebrow">03 — Work</div>
      <h2 class="section-title">Experience</h2>
    </div>
    <div class="exp-item reveal">
      <div class="exp-left">
        <div class="exp-company">SkillCraft Technology</div>
        <div class="exp-period">Mar 2025 — Apr 2025</div>
        <div class="exp-loc">Mumbai · Remote</div>
      </div>
      <div class="exp-right">
        <div class="exp-role">Frontend Developer Intern</div>
        <ul class="exp-bullets">
          <li>Engineered 4 distinct web applications, translating project requirements into functional, responsive user interfaces.</li>
          <li>Built clean, cross-browser compatible codebases with HTML5, CSS3, JavaScript and modern frameworks.</li>
          <li>Implemented efficient data handling and component logic for seamless UX and optimal performance.</li>
          <li>Managed repositories via Git and GitHub with structured commit histories and clean deployment workflows.</li>
        </ul>
        <div class="exp-stack">
          <span class="exp-tag">HTML5</span><span class="exp-tag">CSS3</span><span class="exp-tag">JavaScript</span><span class="exp-tag">Git</span><span class="exp-tag">GitHub</span><span class="exp-tag">Responsive Design</span>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ══ EDUCATION ══ -->
<section id="education">
  <div class="container">
    <div class="reveal">
      <div class="section-eyebrow">04 — Training</div>
      <h2 class="section-title">Education</h2>
    </div>
    <div class="edu-grid reveal">
      <div class="edu-card featured">
        <div class="edu-yr">2024 → 2027</div>
        <div class="edu-deg">Bachelor of Computer Applications (BCA)</div>
        <div class="edu-school">Maharaja Agrasen College, Jagadhri, Haryana</div>
        <div class="edu-badge">Current</div>
      </div>
      <div class="edu-card">
        <div class="edu-yr">2022 → 2023</div>
        <div class="edu-deg">NTC — Computer Operator & Programming Asst.</div>
        <div class="edu-school">Govt. Industrial Training Institute, Yamuna Nagar</div>
        <div class="edu-score">COPA</div>
      </div>
      <div class="edu-card">
        <div class="edu-yr">2021 → 2022</div>
        <div class="edu-deg">Senior Secondary — 12th Grade</div>
        <div class="edu-school">Holy Mother Public School, Yamuna Nagar</div>
        <div class="edu-score">76%</div>
      </div>
      <div class="edu-card">
        <div class="edu-yr">2019 → 2020</div>
        <div class="edu-deg">Secondary — 10th Grade</div>
        <div class="edu-school">Holy Mother Public School, Yamuna Nagar</div>
        <div class="edu-score">83.4%</div>
      </div>
    </div>
  </div>
</section>

<!-- ══ CERTS & AWARDS ══ -->
<section id="certs">
  <div class="container">
    <div class="reveal">
      <div class="section-eyebrow">05 — Credentials</div>
      <h2 class="section-title">Certs &<br>Awards</h2>
    </div>
    <div class="certs-grid">
      <div class="certs-left reveal-left">
        <div class="cert-item">
          <div class="cert-num">01</div>
          <div class="cert-content">
            <div class="cert-name">21st Century Employability Skilling Program</div>
            <div class="cert-by">Wadhwani Foundation · Bengaluru</div>
          </div>
        </div>
        <div class="target-block">
          <div class="target-label">Planned Certifications</div>
          <div class="target-item">CompTIA Security+</div>
          <div class="target-item">CEH — Certified Ethical Hacker</div>
          <div class="target-item">Google Cybersecurity Certificate</div>
          <div class="target-item">eJPT / OSCP (long-term)</div>
        </div>
      </div>
      <div class="awards-block reveal-right" style="transition-delay:.12s">
        <div class="award-row">
          <div class="award-idx">01 — NSS Recognition</div>
          <div class="award-title">Punctuality & Social Service Award</div>
          <div class="award-desc">Recognised by the National Service Scheme for dedicated contribution to community work and punctuality toward responsibilities.</div>
        </div>
        <div class="award-row">
          <div class="award-idx">02 — Competition</div>
          <div class="award-title">1st Place — AI Poster Making (2025–26)</div>
          <div class="award-desc">First position in the AI-themed poster making competition at Maharaja Agrasen College annual event.</div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ══ TERMINAL ══ -->
<section id="terminal-section">
  <div class="container">
    <div class="reveal">
      <div class="section-eyebrow">06 — Interface</div>
      <h2 class="section-title">Terminal</h2>
      <p style="font-size:.8rem;color:rgba(255,255,255,.25);margin-bottom:2rem">Type <code style="color:rgba(0,255,170,.6);background:rgba(0,255,170,.05);padding:.1rem .4rem">help</code> to see all commands</p>
    </div>
    <div class="term-outer reveal">
      <div class="term-bar">
        <div class="tdot r"></div><div class="tdot y"></div><div class="tdot g"></div>
        <div class="term-title-bar">suraj@cybersec — bash — 80×24</div>
        <div class="term-enc">● TLS 1.3</div>
      </div>
      <div class="term-body" id="TOUT">
        <div class="tl"><span class="tii">╔══════════════════════════════════════════╗</span></div>
        <div class="tl"><span class="tii">║  Suraj Bhardwaj — Portfolio Terminal     ║</span></div>
        <div class="tl"><span class="tii">╚══════════════════════════════════════════╝</span></div>
        <div class="tl">&nbsp;</div>
        <div class="tl"><span class="tok">✓</span> <span class="to">Connection secure. Type <span class="tp">help</span> to begin.</span></div>
        <div class="tl">&nbsp;</div>
      </div>
      <div class="term-input-wrap">
        <div class="term-ps1">suraj@cybersec:~$</div>
        <input id="TI" type="text" placeholder="enter command…" autocomplete="off" spellcheck="false">
      </div>
    </div>
  </div>
</section>


<!-- ══ 3D LOCK SCENE ══ -->
<div id="lock-scene-wrap">
  <div id="three-lock"></div>
  <div class="lock-overlay">
    <div class="lock-text-center">
      <div class="lock-tagline">Securing the<br><em>Digital Frontier</em></div>
      <div class="lock-sub">Ethical Hacker in Training · CEH Target 2026</div>
    </div>
  </div>
</div>

<!-- ══ GOAL ══ -->
<section id="goal">
  <div class="container" style="text-align:center">
    <div class="reveal">
      <div class="section-eyebrow" style="justify-content:center">07 — Mission</div>
      <p class="goal-hl">Defending systems.<br>Uncovering <strong>vulnerabilities</strong>.<br>Making the digital world <em>harder to break.</em></p>
    </div>
    <div class="roadmap reveal">
      <div class="rm"><div class="rm-badge a">Active</div><div class="rm-body"><div class="rm-title">BCA — Core CS Foundation</div><div class="rm-desc">Building programming, web dev, and database foundations at Maharaja Agrasen College (2024–2027).</div></div></div>
      <div class="rm"><div class="rm-badge a">Active</div><div class="rm-body"><div class="rm-title">JavaScript & Frontend Mastery</div><div class="rm-desc">Completing JS curriculum — objects, arrays, async, DOM. Targeting full-stack proficiency.</div></div></div>
      <div class="rm"><div class="rm-badge n">Next</div><div class="rm-body"><div class="rm-title">Linux CLI & Networking Fundamentals</div><div class="rm-desc">TCP/IP, file systems, protocols, bash scripting — the bedrock of all security work.</div></div></div>
      <div class="rm"><div class="rm-badge p">Planned</div><div class="rm-body"><div class="rm-title">CompTIA Security+ / CEH Certification</div><div class="rm-desc">Industry-standard credentials to validate cybersecurity skills and open professional doors.</div></div></div>
      <div class="rm"><div class="rm-badge p">Goal</div><div class="rm-body"><div class="rm-title">CTF — HackTheBox / TryHackMe</div><div class="rm-desc">Hands-on penetration testing practice to build real attack-and-defend instincts.</div></div></div>
    </div>
  </div>
</section>

<!-- ══ CONTACT ══ -->
<section id="contact">
  <div class="container">
    <div class="contact-wrap">
      <div class="reveal-left">
        <div class="section-eyebrow">08 — Connect</div>
        <h2 class="section-title">Get In<br>Touch</h2>
        <div class="contact-links">
          <a href="mailto:surajbhardwaaj@gmail.com" class="cc-link"><div class="cc-icon">✉</div><div class="cc-info"><div class="cc-label">Email</div><div class="cc-value">surajbhardwaaj@gmail.com</div></div><div class="cc-arr">↗</div></a>
          <a href="tel:+918396841522" class="cc-link"><div class="cc-icon">☎</div><div class="cc-info"><div class="cc-label">Phone</div><div class="cc-value">+91 83968 41522</div></div><div class="cc-arr">↗</div></a>
          <a href="https://github.com" target="_blank" class="cc-link"><div class="cc-icon" style="font-family:'Syne',sans-serif">GH</div><div class="cc-info"><div class="cc-label">GitHub</div><div class="cc-value">github.com/surajbhardwaj</div></div><div class="cc-arr">↗</div></a>
          <a href="https://linkedin.com" target="_blank" class="cc-link"><div class="cc-icon" style="font-family:'Syne',sans-serif">LI</div><div class="cc-info"><div class="cc-label">LinkedIn</div><div class="cc-value">linkedin.com/in/surajbhardwaj</div></div><div class="cc-arr">↗</div></a>
        </div>
      </div>
      <div class="reveal-right" style="transition-delay:.15s;padding-top:5rem">
        <p class="contact-note">I'm a motivated BCA student seeking <strong>internships, collaborations, and mentorship</strong> in cybersecurity and software development.<br><br>Whether you're a recruiter, a security enthusiast, or someone with an interesting project — reach out. <em>I respond fast.</em></p>
        <div style="font-size:.72rem;color:rgba(255,255,255,.2);letter-spacing:.08em;margin-bottom:1.5rem">📍 Yamunanagar, Haryana, India</div>
        <div class="available-pill" style="font-size:.7rem"><div class="status-blink"></div>Available for opportunities</div>
      </div>
    </div>
  </div>
</section>

<footer>
  <div class="footer-copy">© 2025 Suraj Bhardwaj — All rights reserved</div>
  <div class="footer-tag">Stay curious · Stay ethical · Stay secure</div>
</footer>

<script>
// ── CURSOR ──────────────────────────────────────
const ring=document.getElementById('cursor-ring');
const dot=document.getElementById('cursor-dot');
let mx=0,my=0,rx=0,ry=0;
document.addEventListener('mousemove',e=>{mx=e.clientX;my=e.clientY;dot.style.left=mx+'px';dot.style.top=my+'px'});
(function animCursor(){rx+=(mx-rx)*.18;ry+=(my-ry)*.18;ring.style.left=rx+'px';ring.style.top=ry+'px';requestAnimationFrame(animCursor)})();
document.querySelectorAll('a,button,input,.sc-tag,.skill-item,.award-row,.cc-link').forEach(el=>{
  el.addEventListener('mouseenter',()=>document.body.classList.add('hover-active'));
  el.addEventListener('mouseleave',()=>document.body.classList.remove('hover-active'));
});
document.querySelectorAll('a').forEach(el=>{
  el.addEventListener('mouseenter',()=>document.body.classList.add('link-active'));
  el.addEventListener('mouseleave',()=>document.body.classList.remove('link-active'));
});

// ── HERO CANVAS ─────────────────────────────────
const HC=document.getElementById('hero-canvas');
const HX=HC.getContext('2d');
function rsHero(){HC.width=HC.parentElement.offsetWidth;HC.height=HC.parentElement.offsetHeight}
rsHero();window.addEventListener('resize',rsHero);

// Grid + flowing nodes
const GNodes=[];
for(let i=0;i<55;i++){
  GNodes.push({
    x:Math.random()*HC.width,y:Math.random()*HC.height,
    vx:(Math.random()-.5)*.25,vy:(Math.random()-.5)*.25,
    size:Math.random()>0.92?2.5:1.2,
    pulse:Math.random()*Math.PI*2
  });
}

function drawHero(){
  HX.clearRect(0,0,HC.width,HC.height);
  // subtle grid
  HX.strokeStyle='rgba(255,255,255,.025)';HX.lineWidth=.5;
  const gsize=60;
  for(let x=0;x<HC.width;x+=gsize){HX.beginPath();HX.moveTo(x,0);HX.lineTo(x,HC.height);HX.stroke()}
  for(let y=0;y<HC.height;y+=gsize){HX.beginPath();HX.moveTo(0,y);HX.lineTo(HC.width,y);HX.stroke()}
  // move nodes
  GNodes.forEach(n=>{
    n.pulse+=.02;
    n.x+=n.vx;n.y+=n.vy;
    if(n.x<0||n.x>HC.width)n.vx*=-1;
    if(n.y<0||n.y>HC.height)n.vy*=-1;
  });
  // connections
  GNodes.forEach((a,i)=>{
    GNodes.slice(i+1).forEach(b=>{
      const d=Math.hypot(a.x-b.x,a.y-b.y);
      if(d<130){
        HX.beginPath();HX.moveTo(a.x,a.y);HX.lineTo(b.x,b.y);
        HX.strokeStyle=`rgba(0,255,170,${(1-d/130)*.1})`;
        HX.lineWidth=.5;HX.stroke();
      }
    });
  });
  // nodes
  GNodes.forEach(n=>{
    const alpha=.15+Math.sin(n.pulse)*.07;
    HX.beginPath();HX.arc(n.x,n.y,n.size,0,Math.PI*2);
    HX.fillStyle=n.size>2?`rgba(0,255,170,${alpha*2})`:`rgba(255,255,255,${alpha})`;
    HX.fill();
  });
  // mouse influence
  const mdx=mx,mdy=my;
  HX.beginPath();HX.arc(mdx,mdy,200,0,Math.PI*2);
  const grad=HX.createRadialGradient(mdx,mdy,0,mdx,mdy,200);
  grad.addColorStop(0,'rgba(0,255,170,.04)');
  grad.addColorStop(1,'transparent');
  HX.fillStyle=grad;HX.fill();
  requestAnimationFrame(drawHero);
}
drawHero();

// ── CLOCK ───────────────────────────────────────
const CLK=document.getElementById('NAV-CLK');
function tick(){const t=new Date().toTimeString().slice(0,8);CLK.textContent=t;document.getElementById('TB-time')&&(document.getElementById('TB-time').textContent=t)}
setInterval(tick,1000);tick();

// ── NAV SHOW ────────────────────────────────────
document.getElementById('NAV').style.opacity='1';

// ── SCROLL REVEALS ──────────────────────────────
const revObs=new IntersectionObserver(en=>{
  en.forEach(e=>{if(e.isIntersecting){e.target.classList.add('in');revObs.unobserve(e.target)}});
},{threshold:.07});
document.querySelectorAll('.reveal,.reveal-left,.reveal-right').forEach(el=>revObs.observe(el));

// ── SKILL BARS ──────────────────────────────────
const barObs=new IntersectionObserver(en=>{
  en.forEach(e=>{
    if(e.isIntersecting){
      e.target.querySelectorAll('.skill-bar-fill').forEach(b=>{b.style.width=(b.dataset.w||0)+'%'});
      barObs.unobserve(e.target);
    }
  });
},{threshold:.25});
document.querySelectorAll('.skills-list').forEach(el=>barObs.observe(el));

// ── COUNT-UP ────────────────────────────────────
const cntObs=new IntersectionObserver(en=>{
  en.forEach(e=>{
    if(e.isIntersecting){
      e.target.querySelectorAll('[data-count]').forEach(el=>{
        const target=+el.dataset.count;let cur=0;
        const step=()=>{cur+=1;el.textContent=cur;if(cur<target)setTimeout(step,180/target)};step();
      });
      cntObs.unobserve(e.target);
    }
  });
},{threshold:.3});
document.querySelectorAll('.stat-strip').forEach(el=>cntObs.observe(el));

// ── NAV ACTIVE ──────────────────────────────────
const secs=document.querySelectorAll('section[id]');
const nas=document.querySelectorAll('.nav-links a');
window.addEventListener('scroll',()=>{
  let cur='';
  secs.forEach(s=>{if(window.scrollY>=s.offsetTop-140)cur=s.id});
  nas.forEach(a=>{
    const match=a.getAttribute('href')==='#'+cur;
    a.style.color=match?'rgba(255,255,255,.9)':'rgba(255,255,255,.4)';
  });
});

// ── TERMINAL ────────────────────────────────────
const TOUT=document.getElementById('TOUT'),TIN=document.getElementById('TI');
const HIST=[];let HIDX=-1;
const CMDS={
  help:()=>[
    {c:'tii',v:'┌───────────────────────────────────────┐'},
    {c:'tii',v:'│  COMMANDS                             │'},
    {c:'tii',v:'├───────────────────────────────────────┤'},
    {c:'tii',v:'│  whoami  ·  skills  ·  experience     │'},
    {c:'tii',v:'│  education  ·  certs  ·  goals        │'},
    {c:'tii',v:'│  contact  ·  scan  ·  decode          │'},
    {c:'tii',v:'│  traceroute  ·  nmap  ·  clear        │'},
    {c:'tii',v:'│  cat flag                             │'},
    {c:'tii',v:'└───────────────────────────────────────┘'},
  ],
  whoami:()=>[{c:'tok',v:'USER: Suraj Bhardwaj'},{c:'to',v:'ROLE: Frontend Dev → Cyber Engineer'},{c:'to',v:'LOC : Yamunanagar, Haryana, IN'},{c:'to',v:'EDU : BCA @ Maharaja Agrasen College'},{c:'to',v:'GOAL: CEH / CompTIA Security+'}],
  skills:()=>[{c:'tok',v:'SKILL MATRIX:'},{c:'to',v:'[████████░░] HTML/CSS      88%'},{c:'to',v:'[███████░░░] JavaScript    72%'},{c:'to',v:'[███████░░░] Git/Tools     75%'},{c:'to',v:'[██████░░░░] C/C++         62%'},{c:'to',v:'[██████░░░░] SQL/Oracle    65%'},{c:'ter',v:'[███░░░░░░░] Cybersecurity 28%  ← TRAINING'}],
  experience:()=>[{c:'tok',v:'WORK HISTORY:'},{c:'tii',v:'[2025] SkillCraft Technology — Frontend Intern'},{c:'to',v:'  • 4 web apps built from scratch'},{c:'to',v:'  • HTML5 · CSS3 · JavaScript · Git/GitHub'},{c:'to',v:'  • Mar–Apr 2025 | Mumbai · Remote'}],
  education:()=>[{c:'tok',v:'EDUCATION:'},{c:'tii',v:'[CURRENT] BCA — Maharaja Agrasen College (2024–2027)'},{c:'to',v:'[2023]    COPA NTC — Govt. ITI, Yamuna Nagar'},{c:'to',v:'[2022]    12th Grade — 76%'},{c:'to',v:'[2020]    10th Grade — 83.4%'}],
  certs:()=>[{c:'tok',v:'CREDENTIALS:'},{c:'to',v:'✓ 21st Century Employability — Wadhwani Foundation'},{c:'tok',v:'AWARDS:'},{c:'to',v:'★ NSS Recognition — Punctuality & Social Service'},{c:'to',v:'★ 1st Place — AI Poster Making (2025–26)'}],
  goals:()=>[{c:'tok',v:'ROADMAP:'},{c:'tii',v:'[ACTIVE] BCA + JS mastery'},{c:'tww',v:'[NEXT]   Linux + Networking fundamentals'},{c:'tww',v:'[PLAN]   CompTIA Security+ / CEH'},{c:'ter',v:'[GOAL]   First cybersecurity role by 2027'}],
  contact:()=>[{c:'tok',v:'CONTACT:'},{c:'to',v:'EMAIL  : surajbhardwaaj@gmail.com'},{c:'to',v:'PHONE  : +91 83968 41522'},{c:'to',v:'STATUS : ● AVAILABLE'}],
  scan:()=>[{c:'tok',v:'Scanning target...'},{c:'to',v:'[>] SSL: TLS 1.3 — VALID'},{c:'tww',v:'[!] FINDING: Missing CEH cert (MEDIUM)'},{c:'tww',v:'[!] FINDING: JS proficiency gap (LOW)'},{c:'tok',v:'RESULT: 2 findings, 0 critical'}],
  decode:()=>[{c:'to',v:'HEX: 53 75 72 61 6A 20 42 68 61 72 64 77 61 6A'},{c:'tok',v:'UTF-8: Suraj Bhardwaj'}],
  traceroute:()=>[{c:'tok',v:'Tracing route to career.target...'},{c:'to',v:' 1  HTML/CSS          2ms'},{c:'to',v:' 2  JavaScript         4ms'},{c:'to',v:' 3  Git/DevTools       3ms'},{c:'tww',v:' 4  Networking*       — (learning)'},{c:'ter',v:' 5  Security Certs*   — (planned)'}],
  nmap:()=>[{c:'tok',v:'Nmap scan on suraj.portfolio:'},{c:'to',v:'80/tcp   OPEN  http  (frontend)'},{c:'to',v:'443/tcp  OPEN  https (secure coding)'},{c:'to',v:'22/tcp   OPEN  ssh   (git workflow)'},{c:'tww',v:'4444/tcp FILTERED (security — learning)'}],
  clear:()=>'CLEAR',
  'cat flag':()=>[{c:'tww',v:'Searching...'},{c:'tok',v:'FLAG{5ur4j_1s_4_cyber_w4rr10r}'},{c:'to',v:'You found the easter egg. 🏴'}],
};
function tAdd(cls,txt){const d=document.createElement('div');d.className='tl';d.innerHTML=`<span class="${cls}">${txt}</span>`;TOUT.appendChild(d);TOUT.scrollTop=TOUT.scrollHeight}
TIN.addEventListener('keydown',e=>{
  if(e.key==='ArrowUp'){e.preventDefault();if(HIDX<HIST.length-1){HIDX++;TIN.value=HIST[HIST.length-1-HIDX]}}
  if(e.key==='ArrowDown'){e.preventDefault();if(HIDX>0){HIDX--;TIN.value=HIST[HIST.length-1-HIDX]}else{HIDX=-1;TIN.value=''}}
  if(e.key!=='Enter')return;
  const raw=TIN.value.trim();if(!raw)return;
  HIST.push(raw);HIDX=-1;
  const row=document.createElement('div');row.className='tl';
  row.innerHTML=`<span class="tp">suraj@cybersec:~$</span> <span class="tc">${raw}</span>`;
  TOUT.appendChild(row);TIN.value='';
  const fn=CMDS[raw.toLowerCase()];
  if(!fn){tAdd('ter',`command not found: ${raw}. Type help.`)}
  else{const r=fn();if(r==='CLEAR'){TOUT.innerHTML='';return}r.forEach((v,i)=>setTimeout(()=>tAdd(v.c,v.v),i*55))}
  tAdd('to','');
});

// ═══════════════════════════════════════════════════
//  THREE.JS 1 — HERO: ROTATING 3D SHIELD + PARTICLES
// ═══════════════════════════════════════════════════
(function initHeroThree(){
  const container=document.getElementById('three-hero');
  if(!container||!window.THREE)return;
  const W=container.offsetWidth,H=container.offsetHeight;
  const renderer=new THREE.WebGLRenderer({antialias:true,alpha:true});
  renderer.setSize(W,H);renderer.setPixelRatio(Math.min(devicePixelRatio,2));
  renderer.setClearColor(0x000000,0);
  container.appendChild(renderer.domElement);

  const scene=new THREE.Scene();
  const camera=new THREE.PerspectiveCamera(60,W/H,.1,1000);
  camera.position.set(0,0,5);

  // ── SHIELD geometry (icosahedron = faceted shield feel) ──
  const shieldGeo=new THREE.IcosahedronGeometry(1.4,1);
  const shieldMat=new THREE.MeshBasicMaterial({color:0x00ffaa,wireframe:true,opacity:.18,transparent:true});
  const shield=new THREE.Mesh(shieldGeo,shieldMat);
  shield.position.set(2.8,-.3,0);
  scene.add(shield);

  // inner solid core
  const coreGeo=new THREE.IcosahedronGeometry(.9,0);
  const coreMat=new THREE.MeshBasicMaterial({color:0x00ffaa,wireframe:false,opacity:.04,transparent:true});
  const core=new THREE.Mesh(coreGeo,coreMat);
  core.position.copy(shield.position);
  scene.add(core);

  // outer orbit ring
  const ringGeo=new THREE.TorusGeometry(2.1,.006,8,80);
  const ringMat=new THREE.MeshBasicMaterial({color:0x00ffaa,opacity:.25,transparent:true});
  const ring=new THREE.Mesh(ringGeo,ringMat);ring.position.copy(shield.position);ring.rotation.x=Math.PI/3;
  scene.add(ring);

  const ring2=new THREE.Mesh(new THREE.TorusGeometry(1.7,.004,8,60),new THREE.MeshBasicMaterial({color:0x00aaff,opacity:.15,transparent:true}));
  ring2.position.copy(shield.position);ring2.rotation.y=Math.PI/4;
  scene.add(ring2);

  // orbit nodes (small glowing cubes)
  const nodeGroup=new THREE.Group();nodeGroup.position.copy(shield.position);
  for(let i=0;i<8;i++){
    const a=(i/8)*Math.PI*2;
    const ng=new THREE.BoxGeometry(.07,.07,.07);
    const nm=new THREE.MeshBasicMaterial({color:i%2===0?0x00ffaa:0xff4060,opacity:.7,transparent:true});
    const nb=new THREE.Mesh(ng,nm);
    nb.position.set(Math.cos(a)*2.1,Math.sin(a)*2.1,0);
    nb.userData.angle=a;nb.userData.r=2.1;
    nodeGroup.add(nb);
  }
  scene.add(nodeGroup);

  // left-side floating cubes
  const floaters=[];
  const fcols=[0x00ffaa,0x00aaff,0xff4060,0x44ffcc];
  for(let i=0;i<18;i++){
    const s=.05+Math.random()*.1;
    const fg=new THREE.BoxGeometry(s,s,s);
    const fm=new THREE.MeshBasicMaterial({color:fcols[i%fcols.length],wireframe:Math.random()>.4,opacity:.3+Math.random()*.4,transparent:true});
    const fb=new THREE.Mesh(fg,fm);
    fb.position.set(-3+Math.random()*2.5,(Math.random()-.5)*3.5,(Math.random()-.5)*1.5);
    fb.userData={vx:(Math.random()-.5)*.003,vy:(Math.random()-.5)*.003,rx:(Math.random()-.5)*.01,ry:(Math.random()-.5)*.01};
    scene.add(fb);floaters.push(fb);
  }

  // connection lines between floaters
  const lineMat=new THREE.LineBasicMaterial({color:0x00ffaa,opacity:.06,transparent:true});
  for(let i=0;i<floaters.length;i++){
    for(let j=i+1;j<floaters.length;j++){
      const d=floaters[i].position.distanceTo(floaters[j].position);
      if(d<1.8){
        const pts=[floaters[i].position.clone(),floaters[j].position.clone()];
        const lg=new THREE.BufferGeometry().setFromPoints(pts);
        scene.add(new THREE.Line(lg,lineMat));
      }
    }
  }

  let mouseX=0,mouseY=0;
  document.addEventListener('mousemove',e=>{mouseX=(e.clientX/window.innerWidth-.5)*2;mouseY=-(e.clientY/window.innerHeight-.5)*2;});

  let t=0;
  function animate(){
    requestAnimationFrame(animate);t+=.008;
    shield.rotation.y+=.004;shield.rotation.x+=.002;
    core.rotation.y-=.006;core.rotation.z+=.003;
    ring.rotation.z+=.003;ring2.rotation.x+=.004;ring2.rotation.y+=.002;
    nodeGroup.rotation.z+=.008;
    // mouse parallax
    camera.position.x+=(mouseX*.4-camera.position.x)*.04;
    camera.position.y+=(mouseY*.3-camera.position.y)*.04;
    camera.lookAt(0,0,0);
    // float
    floaters.forEach(f=>{
      f.position.x+=f.userData.vx;f.position.y+=f.userData.vy;
      f.rotation.x+=f.userData.rx;f.rotation.y+=f.userData.ry;
      if(f.position.x<-4||f.position.x>0){f.userData.vx*=-1}
      if(Math.abs(f.position.y)>2.2){f.userData.vy*=-1}
    });
    renderer.render(scene,camera);
  }
  animate();

  window.addEventListener('resize',()=>{
    const nw=container.offsetWidth,nh=container.offsetHeight;
    camera.aspect=nw/nh;camera.updateProjectionMatrix();
    renderer.setSize(nw,nh);
  });
})();

// ═══════════════════════════════════════════════════
//  THREE.JS 2 — GLOBE: WIREFRAME EARTH + THREAT ARCS
// ═══════════════════════════════════════════════════
(function initGlobe(){
  const container=document.getElementById('three-globe');
  if(!container||!window.THREE)return;
  const W=container.offsetWidth,H=container.offsetHeight||600;
  const renderer=new THREE.WebGLRenderer({antialias:true,alpha:true});
  renderer.setSize(W,H);renderer.setPixelRatio(Math.min(devicePixelRatio,2));
  renderer.setClearColor(0x000000,0);
  container.appendChild(renderer.domElement);

  const scene=new THREE.Scene();
  const camera=new THREE.PerspectiveCamera(50,W/H,.1,1000);
  camera.position.set(0,0,3.8);

  // ── Wireframe globe ──
  const globeGeo=new THREE.SphereGeometry(1.5,32,32);
  const globeMat=new THREE.MeshBasicMaterial({color:0x00ffaa,wireframe:true,opacity:.1,transparent:true});
  const globe=new THREE.Mesh(globeGeo,globeMat);
  scene.add(globe);

  // solid inner dark globe
  const innerGeo=new THREE.SphereGeometry(1.48,24,24);
  const innerMat=new THREE.MeshBasicMaterial({color:0x020d0a,opacity:.95,transparent:true});
  scene.add(new THREE.Mesh(innerGeo,innerMat));

  // ── Lat/Lon grid lines ──
  const gridMat=new THREE.LineBasicMaterial({color:0x00ffaa,opacity:.06,transparent:true});
  for(let lat=-80;lat<=80;lat+=20){
    const pts=[];
    for(let lon=0;lon<=360;lon+=5){
      const phi=(90-lat)*Math.PI/180,theta=lon*Math.PI/180;
      pts.push(new THREE.Vector3(1.5*Math.sin(phi)*Math.cos(theta),1.5*Math.cos(phi),1.5*Math.sin(phi)*Math.sin(theta)));
    }
    scene.add(new THREE.Line(new THREE.BufferGeometry().setFromPoints(pts),gridMat));
  }
  for(let lon=0;lon<360;lon+=20){
    const pts=[];
    for(let lat=-90;lat<=90;lat+=5){
      const phi=(90-lat)*Math.PI/180,theta=lon*Math.PI/180;
      pts.push(new THREE.Vector3(1.5*Math.sin(phi)*Math.cos(theta),1.5*Math.cos(phi),1.5*Math.sin(phi)*Math.sin(theta)));
    }
    scene.add(new THREE.Line(new THREE.BufferGeometry().setFromPoints(pts),gridMat));
  }

  // ── City nodes ──
  const cities=[
    [28.6,77.2],[19.1,72.9],[51.5,-0.1],[40.7,-74.0],[35.7,139.7],[55.8,37.6],[1.3,103.8],[48.9,2.3],[-23.5,-46.6],[37.8,144.9]
  ];
  const cityGroup=new THREE.Group();
  cities.forEach(([lat,lon])=>{
    const phi=(90-lat)*Math.PI/180,theta=(lon+180)*Math.PI/180;
    const x=1.52*Math.sin(phi)*Math.cos(theta),y=1.52*Math.cos(phi),z=1.52*Math.sin(phi)*Math.sin(theta);
    const cg=new THREE.SphereGeometry(.025,8,8);
    const cm=new THREE.MeshBasicMaterial({color:0x00ffaa});
    const c=new THREE.Mesh(cg,cm);c.position.set(x,y,z);
    cityGroup.add(c);
    // pulse ring
    const pg=new THREE.RingGeometry(.03,.045,12);
    const pm=new THREE.MeshBasicMaterial({color:0x00ffaa,opacity:.3,transparent:true,side:THREE.DoubleSide});
    const p=new THREE.Mesh(pg,pm);p.position.set(x,y,z);
    p.lookAt(new THREE.Vector3(x*2,y*2,z*2));
    p.userData.pulse=Math.random()*Math.PI*2;
    cityGroup.add(p);
  });
  scene.add(cityGroup);

  // ── Threat arc helpers ──
  function latLonToVec(lat,lon,r){
    const phi=(90-lat)*Math.PI/180,theta=(lon+180)*Math.PI/180;
    return new THREE.Vector3(r*Math.sin(phi)*Math.cos(theta),r*Math.cos(phi),r*Math.sin(phi)*Math.sin(theta));
  }
  function makeCurve(a,b,h){
    const mid=a.clone().add(b).multiplyScalar(.5).normalize().multiplyScalar(1.5+h);
    const curve=new THREE.QuadraticBezierCurve3(a,mid,b);
    return curve.getPoints(40);
  }

  const arcs=[];
  const arcPairs=[[0,4],[1,6],[2,3],[5,7],[0,8],[2,9],[3,6]];
  const arcColors=[0xff4060,0x00ffaa,0xff4060,0xffcc44,0xff4060,0x00aaff,0xff4060];
  arcPairs.forEach(([ai,bi],i)=>{
    const a=latLonToVec(cities[ai][0],cities[ai][1],1.52);
    const b=latLonToVec(cities[bi][0],cities[bi][1],1.52);
    const pts=makeCurve(a,b,.45);
    const geo=new THREE.BufferGeometry().setFromPoints(pts);
    const mat=new THREE.LineBasicMaterial({color:arcColors[i],opacity:.5,transparent:true});
    const line=new THREE.Line(geo,mat);
    scene.add(line);
    // moving dot
    const dotG=new THREE.SphereGeometry(.022,6,6);
    const dotM=new THREE.MeshBasicMaterial({color:arcColors[i]});
    const dot=new THREE.Mesh(dotG,dotM);
    scene.add(dot);
    arcs.push({pts,dot,t:Math.random(),speed:.003+Math.random()*.004});
  });

  // ── Atmosphere glow ring ──
  const atmGeo=new THREE.SphereGeometry(1.6,32,32);
  const atmMat=new THREE.MeshBasicMaterial({color:0x00ffaa,wireframe:false,opacity:.025,transparent:true,side:THREE.BackSide});
  scene.add(new THREE.Mesh(atmGeo,atmMat));

  // auto-rotate + mouse
  let mouseX=0;
  document.addEventListener('mousemove',e=>{mouseX=(e.clientX/window.innerWidth-.5)});
  let t=0;
  function animGlobe(){
    requestAnimationFrame(animGlobe);t+=.005;
    globe.rotation.y+=.002+mouseX*.001;
    cityGroup.rotation.y=globe.rotation.y;
    // pulse rings
    cityGroup.children.forEach(c=>{if(c.userData.pulse!==undefined){c.userData.pulse+=.04;c.scale.setScalar(1+.3*Math.sin(c.userData.pulse));c.material.opacity=.15+.15*Math.sin(c.userData.pulse)}});
    // move threat dots
    arcs.forEach(a=>{
      a.t=(a.t+a.speed)%1;
      const idx=Math.floor(a.t*(a.pts.length-1));
      const p=a.pts[idx];
      // rotate dot with globe
      const rotated=p.clone().applyAxisAngle(new THREE.Vector3(0,1,0),globe.rotation.y);
      a.dot.position.copy(rotated);
    });
    renderer.render(scene,camera);
  }
  animGlobe();

  window.addEventListener('resize',()=>{
    const nw=container.offsetWidth,nh=container.offsetHeight||600;
    camera.aspect=nw/nh;camera.updateProjectionMatrix();renderer.setSize(nw,nh);
  });
})();

// ═══════════════════════════════════════════════════
//  THREE.JS 3 — LOCK SCENE: 3D PADLOCK + PARTICLES
// ═══════════════════════════════════════════════════
(function initLock(){
  const container=document.getElementById('three-lock');
  if(!container||!window.THREE)return;
  const W=container.offsetWidth,H=container.offsetHeight||420;
  const renderer=new THREE.WebGLRenderer({antialias:true,alpha:true});
  renderer.setSize(W,H);renderer.setPixelRatio(Math.min(devicePixelRatio,2));
  renderer.setClearColor(0x000000,0);
  container.appendChild(renderer.domElement);

  const scene=new THREE.Scene();
  const camera=new THREE.PerspectiveCamera(55,W/H,.1,100);
  camera.position.set(0,0,6);

  // ── PADLOCK BODY (rounded box) ──
  const bodyGeo=new THREE.BoxGeometry(1.6,1.4,.6,4,4,2);
  const bodyMat=new THREE.MeshBasicMaterial({color:0x00ffaa,wireframe:true,opacity:.3,transparent:true});
  const body=new THREE.Mesh(bodyGeo,bodyMat);
  body.position.set(0,-.45,0);
  scene.add(body);

  // solid fill
  const bodyFill=new THREE.Mesh(new THREE.BoxGeometry(1.6,1.4,.6),new THREE.MeshBasicMaterial({color:0x020e0a,opacity:.9,transparent:true}));
  bodyFill.position.copy(body.position);scene.add(bodyFill);

  // ── SHACKLE (torus top arc) ──
  const shackleGeo=new THREE.TorusGeometry(.55,.08,12,20,Math.PI);
  const shackleMat=new THREE.MeshBasicMaterial({color:0x00ffaa,wireframe:false,opacity:.6,transparent:true});
  const shackle=new THREE.Mesh(shackleGeo,shackleMat);
  shackle.position.set(0,.35,0);shackle.rotation.z=Math.PI;
  scene.add(shackle);

  // keyhole ring
  const khRing=new THREE.Mesh(new THREE.TorusGeometry(.18,.04,12,24),new THREE.MeshBasicMaterial({color:0x00ffaa,opacity:.5,transparent:true}));
  khRing.position.set(0,-.4,.31);scene.add(khRing);

  // keyhole slot
  const khSlot=new THREE.Mesh(new THREE.CylinderGeometry(.04,.04,.22,8),new THREE.MeshBasicMaterial({color:0x020e0a,opacity:.9,transparent:true}));
  khSlot.position.set(0,-.55,.31);scene.add(khSlot);

  // ── ORBIT RINGS ──
  const orb1=new THREE.Mesh(new THREE.TorusGeometry(2.2,.008,8,80),new THREE.MeshBasicMaterial({color:0x00ffaa,opacity:.15,transparent:true}));
  orb1.rotation.x=Math.PI/2.2;scene.add(orb1);
  const orb2=new THREE.Mesh(new THREE.TorusGeometry(1.7,.005,8,60),new THREE.MeshBasicMaterial({color:0x00aaff,opacity:.1,transparent:true}));
  orb2.rotation.y=Math.PI/3;scene.add(orb2);

  // ── ORBIT DOTS (security nodes) ──
  const orbitDots=[];
  for(let i=0;i<6;i++){
    const a=(i/6)*Math.PI*2;
    const g=new THREE.SphereGeometry(.06,8,8);
    const m=new THREE.MeshBasicMaterial({color:i<2?0xff4060:0x00ffaa,opacity:.8,transparent:true});
    const d=new THREE.Mesh(g,m);
    d.userData={angle:a,r:2.2,tilt:Math.PI/2.2};
    scene.add(d);orbitDots.push(d);
  }

  // ── FLOATING BINARY PLANES (data streams) ──
  const binaryLines=[];
  for(let i=0;i<12;i++){
    const pts=[];
    const startX=-4+Math.random()*8,startY=-3+Math.random()*6;
    for(let j=0;j<6;j++)pts.push(new THREE.Vector3(startX+j*.4,startY,-.5-Math.random()*2));
    const lg=new THREE.BufferGeometry().setFromPoints(pts);
    const lm=new THREE.LineBasicMaterial({color:0x00ffaa,opacity:.06,transparent:true});
    binaryLines.push({line:new THREE.Line(lg,lm),vy:(Math.random()-.5)*.008});
    scene.add(binaryLines[binaryLines.length-1].line);
  }

  // ── PARTICLE FIELD ──
  const pCount=120;
  const pPositions=new Float32Array(pCount*3);
  for(let i=0;i<pCount*3;i++)pPositions[i]=(Math.random()-.5)*10;
  const pGeo=new THREE.BufferGeometry();pGeo.setAttribute('position',new THREE.BufferAttribute(pPositions,3));
  const pMat=new THREE.PointsMaterial({color:0x00ffaa,size:.04,opacity:.35,transparent:true});
  scene.add(new THREE.Points(pGeo,pMat));

  let mouseX=0,mouseY=0;
  document.addEventListener('mousemove',e=>{mouseX=(e.clientX/window.innerWidth-.5);mouseY=-(e.clientY/window.innerHeight-.5);});

  let lockT=0;
  function animLock(){
    requestAnimationFrame(animLock);lockT+=.008;
    body.rotation.y+=.006;body.rotation.x=Math.sin(lockT*.5)*.08;
    bodyFill.rotation.copy(body.rotation);
    shackle.rotation.z=Math.PI+Math.sin(lockT*.7)*.04;shackle.position.y=.35+Math.sin(lockT*.9)*.04;
    khRing.rotation.y+=.006;khSlot.rotation.y+=.006;
    orb1.rotation.z+=.003;orb2.rotation.x+=.004;
    // orbit dot movement
    orbitDots.forEach((d,i)=>{
      d.userData.angle+=.012;
      const a=d.userData.angle,r=d.userData.r,tilt=d.userData.tilt;
      d.position.set(r*Math.sin(a),r*Math.cos(tilt)*Math.cos(a),r*Math.sin(tilt)*Math.cos(a)*.5);
    });
    // binary stream movement
    binaryLines.forEach(b=>{
      b.line.position.y+=b.vy;
      if(Math.abs(b.line.position.y)>4)b.vy*=-1;
    });
    // parallax
    camera.position.x+=(mouseX*.6-camera.position.x)*.05;
    camera.position.y+=(mouseY*.4-camera.position.y)*.05;
    camera.lookAt(0,0,0);
    renderer.render(scene,camera);
  }
  animLock();

  window.addEventListener('resize',()=>{
    const nw=container.offsetWidth,nh=container.offsetHeight||420;
    camera.aspect=nw/nh;camera.updateProjectionMatrix();renderer.setSize(nw,nh);
  });
})();

</script>
</body>
</html>
