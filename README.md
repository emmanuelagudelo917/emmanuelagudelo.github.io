
<html lang="es">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta name="theme-color" content="#102b3f">
  <title>BloodCore | Presentación interactiva</title>
  <style>
    :root {
      --navy:#102b3f; --navy2:#24465b; --paper:#fffefa; --cream:#f6f3ec;
      --ink:#183449; --muted:#5e7484; --line:#dce2e2; --red:#bd263a;
      --red-soft:#f9e3e7; --teal:#d27693; --teal-soft:#fae9ef; --pink-soft:#fae9ef;
      --blue:#286fa8; --blue-soft:#e7f0fa; --gold:#e6ab35; --gold-soft:#fff1d2;
      --green:#39815f; --green-soft:#e7f2e9; --shadow:0 18px 46px rgba(16,43,63,.10);
    }
    *{box-sizing:border-box}
    html{scroll-behavior:smooth;scroll-padding-top:92px}
    body{margin:0;background:var(--cream);color:var(--ink);font-family:Inter,ui-sans-serif,system-ui,-apple-system,"Segoe UI",sans-serif}
    button,a{font:inherit}
    a{color:inherit}
    .topbar{height:68px;position:sticky;top:0;z-index:10;display:flex;align-items:center;justify-content:space-between;gap:18px;padding:0 max(22px,calc((100vw - 1180px)/2));background:rgba(246,243,236,.94);backdrop-filter:blur(12px);border-bottom:1px solid rgba(220,226,226,.8)}
    .brand{display:flex;align-items:center;gap:10px;color:var(--navy);font-size:14px;font-weight:900;letter-spacing:.07em;text-decoration:none}
    .brand-mark{display:grid;place-items:center;width:36px;height:36px;border-radius:11px;background:var(--red-soft);color:var(--red)}
    .brand-mark svg{width:25px;height:25px;display:block}
    .navlinks{display:flex;align-items:center;gap:21px;font-size:13px;font-weight:700;color:var(--muted)}
    .navlinks a{text-decoration:none}.navlinks a:hover{color:var(--red)}
    .score-pill{padding:8px 12px;border:1px solid var(--line);border-radius:999px;background:#fff;color:var(--navy);font-size:13px;font-weight:800;white-space:nowrap}
    .hero{min-height:calc(100vh - 68px);display:grid;align-items:center;overflow:hidden;position:relative;background:radial-gradient(ellipse at 78% 48%,#68101d 0,#310b14 40%,#16080e 78%);color:#fff}
    .hero::before{content:"";position:absolute;width:540px;height:540px;border-radius:50%;right:2%;top:8%;background:radial-gradient(circle,#b9273e 0 31%,#6d1123 32% 52%,rgba(16,43,63,0) 53%);opacity:.56;filter:blur(1px)}
    .hero::after{content:"";position:absolute;inset:0;background:linear-gradient(90deg,rgba(18,5,10,.34),transparent 70%),radial-gradient(ellipse at 92% 10%,rgba(250,90,112,.18),transparent 40%);pointer-events:none}
    .hero-inner{position:relative;z-index:1;width:min(1180px,100%);margin:auto;padding:68px 28px 58px;display:grid;grid-template-columns:1.08fr .92fr;align-items:center;gap:24px}
    .hero-content{position:relative;z-index:2}
    .eyebrow{color:#ff9daf;font-size:12px;font-weight:850;letter-spacing:.16em;text-transform:uppercase}
    .hero h1{max-width:650px;margin:18px 0 6px;font-size:clamp(56px,8vw,98px);line-height:.9;letter-spacing:-.06em;text-transform:uppercase}
    .hero-subtitle{max-width:520px;margin:0 0 18px;color:#ffd8df;font-size:clamp(19px,2.5vw,27px);font-weight:650;line-height:1.2}
    .hero-copy{max-width:540px;margin:0;color:#f3dfe3;font-size:16px;line-height:1.65}
    .hero-actions{display:flex;gap:14px;align-items:center;flex-wrap:wrap;margin-top:30px}
    .btn{display:inline-flex;align-items:center;justify-content:center;gap:9px;min-height:48px;padding:12px 19px;border:1px solid transparent;border-radius:14px;text-decoration:none;font-weight:800;transition:transform .16s ease,background-color .16s ease;cursor:pointer}
    .btn:hover{transform:translateY(-2px)}
    .btn-gold{background:linear-gradient(135deg,#258bd0,#1265ae);color:#fff;box-shadow:0 5px 0 #084776,0 12px 28px #062b554f;border-radius:999px}
    .btn-gold:hover{background:linear-gradient(135deg,#42a8ec,#1676c7)}
    .btn-light{border-color:#587184;color:#fff;background:transparent}
    .btn-light:hover{background:#1b3b51}
    .hero-meta{display:flex;gap:22px;flex-wrap:wrap;margin-top:24px;color:#edcdd3;font-size:13px}
    .hero-meta strong{color:#fff}
    .hero-note{margin-top:18px;color:#ffb2c0;font-size:13px;font-weight:750}
    .cover-credits{display:grid;gap:9px;margin-top:26px;padding-left:14px;border-left:2px solid #e94e68;color:#f0dce0;font-size:12px;line-height:1.45}
    .cover-credits strong{color:#fff}
    .cover-art{position:relative;min-height:430px;display:grid;place-items:center;perspective:900px;isolation:isolate}
    .cover-orbit{position:absolute;width:min(34vw,380px);aspect-ratio:1;border:1px solid #ff9aac55;border-radius:50%;transform:rotateX(68deg) rotateZ(-20deg);box-shadow:0 0 50px #ed355222,inset 0 0 36px #ed355222}
    .cover-orbit::before,.cover-orbit::after{content:"";position:absolute;inset:12%;border:1px solid #ff9aac35;border-radius:50%}
    .cover-orbit::after{inset:-13%;transform:rotateY(66deg)}
    .blood-drop{position:relative;width:235px;height:290px;filter:drop-shadow(0 35px 24px #0902078c);transform:rotate(-8deg);animation:drop-float 5s ease-in-out infinite}
    .drop-shape{position:absolute;inset:0;border-radius:54% 46% 58% 42% / 68% 68% 32% 32%;transform:rotate(45deg) scale(.84);background:radial-gradient(ellipse at 30% 24%,#ff9a9d 0 3%,#f34e63 12%,#b91230 36%,#6d071c 66%,#2d0711 100%);box-shadow:inset -18px -20px 35px #320510,inset 14px 10px 25px #ffb4b54f,0 0 50px #ec264c55}
    .drop-shape::after{content:"";position:absolute;width:56%;height:28%;left:15%;top:19%;border-radius:50%;transform:rotate(-35deg);background:linear-gradient(130deg,#ffffff70,transparent 72%);filter:blur(5px)}
    .drop-cell{position:absolute;border-radius:50%;background:radial-gradient(ellipse at 32% 26%,#ffb4b8,#ed5367 38%,#9a1028 75%,#5c0819);box-shadow:inset -7px -8px 12px #4b0715,inset 4px 4px 9px #ffd0d055,0 8px 12px #27030e99}
    .drop-cell::after{content:"";position:absolute;inset:32%;border-radius:50%;background:radial-gradient(circle,#870b24,#4a0717 75%);box-shadow:inset 2px 3px 5px #21020a}
    .drop-cell.c1{width:92px;height:65px;left:28px;top:92px;transform:rotate(-20deg)}
    .drop-cell.c2{width:72px;height:52px;right:28px;top:145px;transform:rotate(22deg)}
    .drop-cell.c3{width:58px;height:43px;left:73px;bottom:42px;transform:rotate(12deg)}
    .drop-cell.c4{width:50px;height:36px;right:50px;top:55px;transform:rotate(-12deg);opacity:.86}
    .plasma-dot{position:absolute;width:18px;height:18px;border-radius:50%;background:radial-gradient(circle at 30% 25%,#fff4d5,#f4b4bd 35%,#b94868 76%);box-shadow:0 0 18px #ffc2d977}
    .plasma-dot.p1{left:12%;top:30%}.plasma-dot.p2{right:12%;bottom:28%;width:12px;height:12px}.plasma-dot.p3{right:23%;top:19%;width:10px;height:10px}
    .art-label{position:absolute;right:3%;bottom:12%;padding:10px 14px;border:1px solid #ffcfda48;border-radius:14px;background:#210911aa;color:#ffe0e5;font-size:11px;font-weight:750;letter-spacing:.06em;backdrop-filter:blur(8px)}
    @keyframes drop-float{0%,100%{transform:rotate(-8deg) translateY(0)}50%{transform:rotate(-4deg) translateY(-12px)}}
    #funciones .chapter,#componentes .chapter,#hematopoyesis .chapter,#eritrocitos .chapter,#defensa-hemostasia .chapter,#casos .chapter{color:var(--red)}
    #funciones .chapter-num,#componentes .chapter-num,#hematopoyesis .chapter-num,#eritrocitos .chapter-num,#defensa-hemostasia .chapter-num,#casos .chapter-num{background:var(--red-soft);color:var(--red)}
    #bioingenieria .chapter{color:var(--blue)}
    #bioingenieria .chapter-num{background:var(--blue-soft);color:var(--blue)}
    #bioingenieria .callout{border-color:var(--blue);background:var(--blue-soft);color:#174a72}
    #bioingenieria .flow-arrow{color:var(--blue)}
    #bioingenieria .flow-node{background:var(--blue-soft)}
    #bioingenieria .flow-node.red{background:var(--pink-soft)}
    #bioingenieria .flow-node.teal{background:var(--blue-soft)}
    #bioingenieria .flow-node.gold{background:var(--pink-soft)}
    #bioingenieria .tech{border-left:3px solid var(--blue)}
    main{width:min(1180px,100%);margin:auto;padding:20px 28px 0}
    .section{padding:80px 0;border-bottom:1px solid var(--line)}
    .section-head{max-width:790px;margin-bottom:34px}
    .chapter{display:flex;align-items:center;gap:10px;margin-bottom:12px;color:var(--teal);font-size:12px;font-weight:850;letter-spacing:.1em;text-transform:uppercase}
    .chapter-num{display:grid;place-items:center;width:29px;height:29px;border-radius:50%;background:var(--teal-soft);letter-spacing:0}
    h2{margin:0;color:var(--navy);font-size:clamp(32px,4vw,48px);letter-spacing:-.035em;line-height:1.06}
    .lead{margin:15px 0 0;color:var(--muted);font-size:18px;line-height:1.6}
    .function-grid{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:18px}
    .function{min-height:183px;padding:21px 19px;border-top:4px solid var(--accent);background:rgba(255,254,250,.75)}
    .function-icon{display:grid;place-items:center;width:39px;height:39px;margin-bottom:15px;border-radius:13px;color:var(--accent);background:var(--tint);font-size:19px;font-weight:900}
    .function h3,.plain-panel h3{margin:0 0 7px;color:var(--navy);font-size:18px}
    .function p,.plain-panel p{margin:0;color:var(--muted);font-size:14px;line-height:1.55}
    .composition{display:grid;grid-template-columns:.75fr 1fr 1fr;gap:16px;align-items:stretch}
    .blood-root{display:grid;place-items:center;min-height:250px;padding:24px;border-radius:22px;background:var(--navy);color:#fff;text-align:center}
    .drop{width:58px;height:58px;display:grid;place-items:center;margin-bottom:12px;border-radius:50% 50% 45% 45%;background:var(--red);font-size:25px}
    .blood-root strong{font-size:23px}.blood-root span{color:#cfdee5;font-size:13px}
    .branch{position:relative;padding:24px;border-radius:22px;background:var(--paper);border:1px solid var(--line)}
    .branch-label{display:inline-flex;padding:7px 11px;border-radius:999px;font-size:11px;font-weight:850;letter-spacing:.06em;text-transform:uppercase}
    .branch.plasma .branch-label{color:#875d08;background:var(--gold-soft)}
    .branch.cells .branch-label{color:#a52731;background:var(--red-soft)}
    .branch h3{margin:19px 0 8px;color:var(--navy);font-size:22px}
    .branch>p{margin:0 0 17px;color:var(--muted);font-size:14px;line-height:1.55}
    .list{display:grid;gap:10px;margin:0;padding:0;list-style:none}
    .list li{display:flex;gap:9px;align-items:flex-start;font-size:14px;line-height:1.45}
    .list li::before{content:"";width:8px;height:8px;flex:0 0 8px;margin-top:6px;border-radius:50%;background:var(--accent,var(--teal))}
    .callout{margin-top:19px;padding:14px 16px;border-left:3px solid var(--teal);background:var(--teal-soft);color:#175c58;font-size:14px;font-weight:700;line-height:1.5}
    .flow{display:flex;align-items:center;gap:10px;flex-wrap:wrap;margin:25px 0;padding:21px;border-radius:20px;background:var(--paper);border:1px solid var(--line)}
    .flow-node{padding:11px 14px;border-radius:12px;background:var(--blue-soft);color:var(--navy);font-size:14px;font-weight:800}
    .flow-node.red{background:var(--red-soft)}.flow-node.teal{background:var(--teal-soft)}.flow-node.gold{background:var(--gold-soft)}
    .flow-arrow{color:var(--red);font-weight:900}
    .two-col{display:grid;grid-template-columns:1fr 1fr;gap:24px;align-items:start}
    .plain-panel{padding:25px;border-radius:22px;background:var(--paper);border:1px solid var(--line)}
    .plain-panel .list{margin-top:17px}
    .stem-cell{display:inline-flex;align-items:center;gap:11px;padding:12px 15px;border:1px solid #b8ddd7;border-radius:14px;background:var(--teal-soft);color:#175c58;font-weight:800}
    .stem-dot{width:18px;height:18px;border-radius:50%;background:var(--teal);box-shadow:0 0 0 5px #c2e4df}
    .feature-row{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:16px;margin-top:24px}
    .feature{padding:21px;border-radius:19px;background:var(--paper);border:1px solid var(--line)}
    .feature .n{display:grid;place-items:center;width:34px;height:34px;margin-bottom:13px;border-radius:50%;background:var(--accent);color:#fff;font-size:14px;font-weight:850}
    .feature h3{margin:0 0 7px;color:var(--navy);font-size:16px}
    .feature p{margin:0;color:var(--muted);font-size:14px;line-height:1.5}
    .rbc-visual{display:grid;grid-template-columns:minmax(210px,.8fr) minmax(270px,1.2fr);gap:20px;align-items:center;margin:28px 0;padding:24px;border-radius:22px;background:linear-gradient(120deg,var(--red-soft),#fff 64%,var(--teal-soft));border:1px solid #eed3d9}
    .rbc-visual-copy .eyebrow{color:var(--red);font-size:11px}
    .rbc-visual-copy h3{margin:9px 0 8px;color:var(--navy);font-size:24px}
    .rbc-visual-copy p{margin:0;color:var(--muted);font-size:14px;line-height:1.55}
    .rbc-visual-copy .caption{display:block;margin-top:12px;color:#8b6270;font-size:11px}
    .scene{position:relative;min-height:240px;display:grid;place-items:center;perspective:780px;overflow:hidden}
    .vessel{position:absolute;width:min(390px,90%);height:136px;border:19px solid rgba(210,118,147,.52);border-radius:50%;transform:rotateX(58deg) rotateZ(-8deg);box-shadow:inset 0 0 0 2px rgba(189,38,58,.08),0 16px 28px rgba(97,36,53,.11)}
    .vessel::before,.vessel::after{content:"";position:absolute;left:50%;width:76%;height:22px;border-radius:50%;transform:translateX(-50%)}
    .vessel::before{top:-25px;background:rgba(255,255,255,.65)}.vessel::after{bottom:-25px;background:rgba(189,38,58,.12)}
    .erythrocyte{position:relative;z-index:1;width:153px;height:153px;border-radius:50%;transform:rotateX(64deg) rotateZ(-18deg);transform-style:preserve-3d;background:radial-gradient(ellipse at 50% 48%,#751324 0 13%,#a61b30 26%,#d83a4b 48%,#ed6470 64%,#b51e32 84%,#801526 100%);box-shadow:inset 0 17px 22px rgba(255,159,164,.74),inset 0 -17px 22px rgba(76,0,12,.45),0 22px 27px rgba(74,13,26,.24)}
    .erythrocyte::after{content:"";position:absolute;inset:14px;border-radius:50%;border:1px solid rgba(255,197,198,.42);transform:translateZ(2px)}
    .erythrocyte.rotate-once{animation:cell-rotate 1.15s cubic-bezier(.2,.75,.2,1) both}
    @keyframes cell-rotate{0%{transform:rotateX(64deg) rotateZ(-18deg)}55%{transform:rotateX(18deg) rotateY(175deg) rotateZ(120deg) scale(1.08)}100%{transform:rotateX(64deg) rotateY(360deg) rotateZ(342deg)}}
    .scene-control{position:absolute;z-index:2;right:4px;bottom:2px;padding:8px 11px;border:1px solid #e6bbc5;border-radius:10px;background:#fff;color:var(--red);font-size:12px;font-weight:800;cursor:pointer}
    .scene-control:hover{background:var(--red-soft)}
    .sequence{display:grid;grid-template-columns:repeat(6,minmax(0,1fr));gap:0;margin-top:24px}
    .seq-step{position:relative;padding:18px 12px 14px;text-align:center}
    .seq-step:not(:last-child)::after{content:"→";position:absolute;right:-8px;top:24px;color:#8a9aa4;font-weight:900}
    .seq-dot{width:42px;height:42px;display:grid;place-items:center;margin:0 auto 10px;border-radius:50%;background:var(--tint);color:var(--accent);font-weight:900}
    .seq-step strong{font-size:13px;color:var(--navy)}
    .cases{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:14px}
    .case{padding:18px 19px;border-left:4px solid var(--accent);background:var(--paper)}
    .case h3{margin:0 0 6px;color:var(--accent);font-size:13px;letter-spacing:.05em;text-transform:uppercase}
    .case p{margin:0;color:var(--muted);font-size:14px;line-height:1.48}
    .tech-map{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:11px;margin-top:22px}
    .tech{padding:14px 15px;border-radius:13px;background:#fff;border:1px solid var(--line);font-size:13px;color:var(--ink)}
    .tech strong{display:block;margin-bottom:4px;color:var(--navy);font-size:14px}
    .quiz-section{padding:82px 0 70px}
    .quiz-intro{display:flex;justify-content:space-between;align-items:end;gap:20px;flex-wrap:wrap;margin-bottom:30px}
    .quiz-title{max-width:670px}
    .quiz-title h2{font-size:clamp(34px,4.5vw,54px)}
    .quiz-title p{max-width:640px;margin:13px 0 0;color:var(--muted);font-size:17px;line-height:1.55}
    .quiz-score{padding:13px 16px;border-radius:15px;background:var(--navy);color:#fff;font-weight:850;white-space:nowrap}
    .score-pulse{display:inline-block;animation:score-pulse .42s ease-out}
    @keyframes score-pulse{0%{transform:scale(.75);color:#ffc95c}65%{transform:scale(1.2);color:#fff}100%{transform:scale(1);color:inherit}}
    .star-reward{display:inline-flex;align-items:center;gap:4px;margin-left:6px;color:#8a5b00;font-weight:900;animation:star-award .62s cubic-bezier(.18,.8,.25,1.3) both}
    @keyframes star-award{0%{transform:scale(.4) rotate(-20deg);opacity:0}75%{transform:scale(1.22) rotate(7deg);opacity:1}100%{transform:scale(1) rotate(0)}}
    .quiz-meter{height:8px;margin:16px 0 30px;border-radius:999px;background:#e5eae7;overflow:hidden}
    .quiz-meter span{display:block;width:0;height:100%;border-radius:inherit;background:linear-gradient(90deg,var(--red),#f3976f);transition:width .25s ease}
    .questions{display:grid;gap:15px}
    .question{padding:22px 23px;border-radius:20px;background:var(--paper);border:1px solid var(--line);scroll-margin-top:90px}
    .q-head{display:flex;align-items:center;gap:11px;margin-bottom:12px}
    .q-num{display:grid;place-items:center;width:31px;height:31px;border-radius:10px;background:var(--red-soft);color:var(--red);font-weight:900;font-size:12px}
    .q-station{color:var(--teal);font-size:11px;text-transform:uppercase;letter-spacing:.09em;font-weight:900}
    .question h3{margin:0 0 8px;color:var(--navy);font-size:20px;line-height:1.3}
    .question>p{margin:0 0 15px;color:var(--muted);font-size:14px;line-height:1.5}
    .answers{display:grid;gap:9px}
    .answer{display:flex;align-items:flex-start;gap:10px;width:100%;padding:12px 13px;border:1px solid var(--line);border-radius:12px;background:#fff;color:var(--ink);font-size:14px;line-height:1.45;text-align:left;cursor:pointer;transition:background-color .14s,border-color .14s}
    .answer:hover:not(:disabled){border-color:#85b9b2;background:#f7fcfa}
    .answer-letter{display:grid;place-items:center;width:23px;height:23px;flex:0 0 23px;border-radius:7px;background:#edf2f1;color:var(--muted);font-size:11px;font-weight:900}
    .answer.correct{border-color:#70b59a;background:var(--green-soft)}.answer.correct .answer-letter{background:var(--green);color:#fff}
    .answer.incorrect{border-color:#e38d89;background:#fff5f3}.answer.incorrect .answer-letter{background:var(--red);color:#fff}
    .answer:disabled{cursor:default}
    .q-feedback{margin-top:12px;padding:12px 14px;border-radius:12px;font-size:13px;line-height:1.5}
    .q-feedback.good{background:var(--green-soft);color:#215c46}.q-feedback.retry{background:var(--gold-soft);color:#80561c}
    .q-feedback strong{display:block;margin-bottom:2px}
    .q-actions{display:flex;gap:10px;align-items:center;margin-top:12px;flex-wrap:wrap}
    .small-btn{min-height:38px;padding:8px 12px;border:1px solid var(--line);border-radius:10px;background:#fff;color:var(--navy);font-size:12px;font-weight:800;cursor:pointer}
    .small-btn:hover{background:var(--teal-soft)}.small-btn:disabled{opacity:.55;cursor:default}
    .hint{color:var(--muted);font-size:12px}
    .answer:focus-visible,.btn:focus-visible,.small-btn:focus-visible,a:focus-visible{outline:3px solid #78c9c1;outline-offset:3px}
    .footer{width:min(1180px,100%);margin:auto;padding:20px 28px 30px;display:flex;justify-content:space-between;gap:12px;flex-wrap:wrap;color:#778892;font-size:12px}
    @media(max-width:900px){.function-grid{grid-template-columns:repeat(2,minmax(0,1fr))}.composition{grid-template-columns:1fr 1fr}.blood-root{grid-column:1/-1;min-height:145px}.cases{grid-template-columns:repeat(2,minmax(0,1fr))}.tech-map{grid-template-columns:repeat(2,minmax(0,1fr))}.hero::before{right:-100px;opacity:.52}}
    @media(max-width:820px){.hero-inner{grid-template-columns:1fr .82fr;gap:4px}.cover-art{min-height:360px}.blood-drop{transform:scale(.83) rotate(-8deg)}.art-label{right:0;bottom:7%}}
    @media(max-width:620px){.topbar{padding:0 16px}.navlinks{gap:11px}.navlinks a:not(:last-child){display:none}.score-pill{font-size:11px;padding:7px 9px}.hero{min-height:calc(92vh - 68px)}.hero-inner{grid-template-columns:1fr;padding:45px 22px 32px;gap:0}.hero::before{width:300px;height:300px;right:-132px;top:4%;opacity:.42}.hero h1{font-size:52px;max-width:400px}.hero-copy{font-size:16px}.hero-meta{gap:12px}.hero-note{max-width:270px}.cover-art{min-height:265px;margin-top:-2px}.cover-orbit{width:220px}.blood-drop{transform:scale(.68) rotate(-8deg)}.art-label{right:4%;bottom:5%;font-size:9px}main{padding:8px 18px 0}.section{padding:58px 0}.section-head{margin-bottom:24px}.lead{font-size:16px}.function-grid{gap:10px}.function{min-height:176px;padding:16px 14px}.function p,.plain-panel p,.list li,.case p{font-size:13px}.composition{grid-template-columns:1fr}.blood-root{grid-column:auto;min-height:150px}.two-col{grid-template-columns:1fr;gap:13px}.plain-panel{padding:20px}.feature-row{grid-template-columns:1fr;gap:10px}.feature{padding:17px}.rbc-visual{grid-template-columns:1fr;padding:20px}.scene{min-height:215px}.sequence{grid-template-columns:repeat(3,minmax(0,1fr));row-gap:10px}.seq-step:nth-child(3)::after{display:none}.cases{grid-template-columns:1fr}.tech-map{grid-template-columns:1fr 1fr;gap:8px}.tech{padding:12px}.quiz-section{padding:60px 0 45px}.quiz-title p{font-size:15px}.question{padding:18px 15px}.question h3{font-size:18px}.answer{font-size:13px}.footer{padding:15px 18px 24px}}
    @media(prefers-reduced-motion:reduce){*,*::before,*::after{scroll-behavior:auto!important;transition:none!important}}
  </style>
</head>
<body>
  <header class="topbar">
    <a class="brand" href="#inicio" aria-label="BloodCore, inicio"><span class="brand-mark" aria-hidden="true"><svg viewBox="0 0 24 24" role="img"><path fill="currentColor" d="M12 1.8S4.1 10.3 4.1 15.3a7.9 7.9 0 0 0 15.8 0C19.9 10.3 12 1.8 12 1.8Z"/><path fill="#fff" opacity=".78" d="M8 15.1c.2-1.6 1.2-3.3 2.1-4.6-.3 2-.1 3.1 1.3 4.2 1.2.9 1.8 1.6 1.7 2.6-.1 1.4-1.3 2.4-2.7 2.4-1.8 0-2.8-1.9-2.4-4.6Z"/></svg></span><span>BloodCore</span></a>
    <nav class="navlinks" aria-label="Navegación principal"><a href="#recorrido">Recorrido</a><a href="#preguntas">Preguntas</a><span class="score-pill">⭐ <span id="stars-live">0</span> <span class="desktop-label">estrellas · </span><span id="score-live">0</span> pts</span></nav>
  </header>

  <section class="hero" id="inicio" aria-labelledby="hero-title">
    <div class="hero-inner">
      <div class="hero-content">
        <div class="eyebrow">BloodCore · Ingeniería biomédica</div>
        <h1 id="hero-title">Sangre</h1>
        <p class="hero-subtitle">Del tejido vivo a la información clínica</p>
        <p class="hero-copy">Descubre cómo sus células mantienen la vida y cómo la ingeniería biomédica transforma una muestra en información útil.</p>
        <div class="cover-credits"><span><strong>Ingeniería Biomédica · ITM</strong></span><span>Estudiante: <strong>Valeria Cadavid Hincapie</strong></span><span>Docente: <strong>Alejandro Vargas Gutiérrez, M.D., MSc.</strong></span></div>
        <div class="hero-actions"><a class="btn btn-gold" href="#recorrido">Explorar la sangre <span aria-hidden="true">➜</span></a><a class="btn btn-light" href="#preguntas">Ir al reto final <span aria-hidden="true">→</span></a></div>
        <div class="hero-note">Explora el recorrido y gana estrellas con cada respuesta correcta.</div>
      </div>
      <div class="cover-art" role="img" aria-label="Ilustración 3D estilizada de una gota de sangre con eritrocitos y componentes en suspensión">
        <div class="cover-orbit" aria-hidden="true"></div><div class="blood-drop" aria-hidden="true"><div class="drop-shape"></div><span class="drop-cell c1"></span><span class="drop-cell c2"></span><span class="drop-cell c3"></span><span class="drop-cell c4"></span><i class="plasma-dot p1"></i><i class="plasma-dot p2"></i><i class="plasma-dot p3"></i></div><div class="art-label">CÉLULAS EN CIRCULACIÓN · VISTA 3D</div>
      </div>
    </div>
  </section>

  <main id="recorrido">
    <section class="section" id="funciones">
      <div class="section-head"><div class="chapter"><span class="chapter-num">01</span> Una mirada general</div><h2>La sangre conecta el cuerpo</h2><p class="lead">Es un tejido dinámico que transporta sustancias, comunica órganos, participa en la defensa y ayuda a regular el equilibrio interno.</p></div>
      <div class="function-grid">
        <article class="function" style="--accent:var(--red);--tint:var(--red-soft)"><span class="function-icon">↔</span><h3>Transporta</h3><p>Oxígeno, CO₂, nutrientes, hormonas, desechos y medicamentos.</p></article>
        <article class="function" style="--accent:var(--teal);--tint:var(--teal-soft)"><span class="function-icon">◎</span><h3>Defiende</h3><p>Leucocitos, anticuerpos y otras respuestas protegen al organismo.</p></article>
        <article class="function" style="--accent:var(--blue);--tint:var(--blue-soft)"><span class="function-icon">≈</span><h3>Regula</h3><p>Ayuda a mantener temperatura, pH, volumen y equilibrio de electrolitos.</p></article>
        <article class="function" style="--accent:var(--gold);--tint:var(--gold-soft)"><span class="function-icon">＋</span><h3>Repara</h3><p>Plaquetas y factores de coagulación participan en la hemostasia.</p></article>
      </div>
      <div class="callout">Idea clave: sangre = transporte + comunicación + defensa + regulación + reparación.</div>
    </section>

    <section class="section" id="componentes">
      <div class="section-head"><div class="chapter"><span class="chapter-num">02</span> Mapa conceptual</div><h2>¿Qué hay dentro de la sangre?</h2><p class="lead">El esquema se divide en dos ramas: el plasma y los elementos formes. Cada parte aporta una función distinta.</p></div>
      <div class="composition">
        <div class="blood-root"><span class="drop" aria-hidden="true">●</span><strong>SANGRE</strong><span>Tejido conectivo especializado</span></div>
        <article class="branch plasma"><span class="branch-label">Parte líquida</span><h3>Plasma</h3><p>Es el medio donde viajan muchas sustancias.</p><ul class="list" style="--accent:var(--gold)"><li>Agua y proteínas</li><li>Electrolitos y nutrientes</li><li>Hormonas y productos de desecho</li></ul></article>
        <article class="branch cells"><span class="branch-label">Células y fragmentos</span><h3>Elementos formes</h3><p>Sus componentes tienen trabajos especializados.</p><ul class="list" style="--accent:var(--red)"><li>Eritrocitos: transporte de gases</li><li>Leucocitos: defensa</li><li>Plaquetas: hemostasia</li></ul></article>
      </div>
      <div class="callout">Para leer el mapa: sangre → plasma + elementos formes → función de cada componente.</div>
    </section>

    <section class="section" id="hematopoyesis">
      <div class="section-head"><div class="chapter"><span class="chapter-num">03</span> Origen celular</div><h2>Hematopoyesis: dónde nacen las células</h2><p class="lead">La médula ósea produce células sanguíneas. Una célula madre hematopoyética puede diferenciarse en líneas celulares con funciones distintas.</p></div>
      <div class="stem-cell"><span class="stem-dot" aria-hidden="true"></span>Célula madre hematopoyética</div>
      <div class="flow" role="img" aria-label="Mapa: médula ósea, célula madre, diferenciación y células sanguíneas">
        <span class="flow-node teal">Médula ósea</span><span class="flow-arrow">→</span><span class="flow-node">Célula madre</span><span class="flow-arrow">→</span><span class="flow-node gold">Diferenciación</span><span class="flow-arrow">→</span><span class="flow-node red">Células sanguíneas</span>
      </div>
      <div class="two-col">
        <article class="plain-panel"><h3>Linaje mieloide</h3><p>Incluye eritrocitos, varios leucocitos y plaquetas.</p><ul class="list" style="--accent:var(--red)"><li>Eritrocitos: transportan oxígeno</li><li>Neutrófilos, eosinófilos, basófilos y monocitos: participan en defensa</li><li>Plaquetas: coagulación y reparación de vasos</li></ul></article>
        <article class="plain-panel"><h3>Linaje linfoide</h3><p>Incluye tipos de linfocitos con tareas inmunitarias.</p><ul class="list" style="--accent:var(--teal)"><li>Linfocitos T: inmunidad celular</li><li>Linfocitos B: producción de anticuerpos</li><li>Linfocitos NK: destrucción de algunas células infectadas o tumorales</li></ul></article>
      </div>
    </section>

    <section class="section" id="eritrocitos">
      <div class="section-head"><div class="chapter"><span class="chapter-num">04</span> Transporte de gases</div><h2>Eritrocitos: células al servicio del oxígeno</h2><p class="lead">Una pregunta de morfofisiología: ¿cómo puede una célula sin núcleo transportar oxígeno durante aproximadamente 120 días?</p></div>
      <div class="flow" role="img" aria-label="El oxígeno viaja desde los pulmones unido a la hemoglobina hasta los tejidos">
        <span class="flow-node red">Pulmones</span><span class="flow-arrow">→</span><span class="flow-node">Hemoglobina en eritrocitos</span><span class="flow-arrow">→</span><span class="flow-node teal">Tejidos</span>
      </div>
      <div class="rbc-visual">
        <div class="rbc-visual-copy"><div class="eyebrow">Modelo tridimensional</div><h3>El eritrocito en la microcirculación</h3><p>Su forma bicóncava y su flexibilidad ayudan a pasar por vasos estrechos. Gira el modelo para observarlo desde otro ángulo.</p><span class="caption">Ilustración esquemática; no está a escala.</span></div>
        <div class="scene" role="img" aria-label="Ilustración 3D esquemática de un eritrocito bicóncavo dentro de un vaso sanguíneo"><div class="vessel" aria-hidden="true"></div><div class="erythrocyte" id="rbc-model" aria-hidden="true"></div><button class="scene-control" id="rotate-model" type="button">↻ Girar eritrocito</button></div>
      </div>
      <div class="feature-row">
        <article class="feature" style="--accent:var(--red)"><span class="n">1</span><h3>Hemoglobina</h3><p>Se une al oxígeno en los pulmones y lo libera en los tejidos.</p></article>
        <article class="feature" style="--accent:var(--blue)"><span class="n">2</span><h3>Deformabilidad</h3><p>El eritrocito cambia de forma para atravesar vasos muy estrechos.</p></article>
        <article class="feature" style="--accent:var(--teal)"><span class="n">3</span><h3>Medición</h3><p>Hemoglobina y hematocrito ayudan a evaluar el transporte de oxígeno.</p></article>
      </div>
      <div class="callout">Conexión biomédica: microcirculación, analizadores hematológicos y hemoglobinómetros.</div>
    </section>

    <section class="section" id="defensa-hemostasia">
      <div class="section-head"><div class="chapter"><span class="chapter-num">05</span> Defensa y reparación</div><h2>Dos trabajos de la sangre en acción</h2><p class="lead">Los leucocitos circulan como parte de la defensa. Cuando un vaso se lesiona, plaquetas y factores de coagulación ayudan a contener la pérdida de sangre.</p></div>
      <div class="two-col">
        <article class="plain-panel"><h3>Defensa circulante</h3><p>El mapa identifica distintos tipos de leucocitos:</p><ul class="list" style="--accent:var(--teal)"><li>Neutrófilos</li><li>Linfocitos</li><li>Monocitos</li><li>Eosinófilos y basófilos</li></ul><div class="callout">La sangre funciona como vía de movilización y comunicación del sistema inmune.</div></article>
        <article class="plain-panel"><h3>Hemostasia</h3><p>La respuesta se organiza en una secuencia:</p><div class="sequence" aria-label="Lesión, activación plaquetaria, coagulación, fibrina, coágulo y reparación">
          <div class="seq-step" style="--accent:var(--red);--tint:var(--red-soft)"><span class="seq-dot">1</span><strong>Lesión</strong></div><div class="seq-step" style="--accent:var(--gold);--tint:var(--gold-soft)"><span class="seq-dot">2</span><strong>Plaquetas</strong></div><div class="seq-step" style="--accent:var(--blue);--tint:var(--blue-soft)"><span class="seq-dot">3</span><strong>Coagulación</strong></div><div class="seq-step" style="--accent:var(--teal);--tint:var(--teal-soft)"><span class="seq-dot">4</span><strong>Fibrina</strong></div><div class="seq-step" style="--accent:var(--red);--tint:var(--red-soft)"><span class="seq-dot">5</span><strong>Coágulo</strong></div><div class="seq-step" style="--accent:var(--green);--tint:var(--green-soft)"><span class="seq-dot">6</span><strong>Reparación</strong></div>
        </div><div class="callout">Si el equilibrio falla, puede haber sangrado excesivo o trombosis.</div></article>
      </div>
    </section>

    <section class="section" id="casos">
      <div class="section-head"><div class="chapter"><span class="chapter-num">06</span> Cuando algo cambia</div><h2>Una alteración deja una huella medible</h2><p class="lead">Relaciona cada problema biológico con la variable que podría ayudar a describirlo.</p></div>
      <div class="cases">
        <article class="case" style="--accent:var(--red)"><h3>Anemia</h3><p>Menor concentración de hemoglobina y menor capacidad de transportar oxígeno.</p></article>
        <article class="case" style="--accent:var(--blue)"><h3>Policitemia</h3><p>Aumento de la masa eritrocitaria; puede cambiar la viscosidad.</p></article>
        <article class="case" style="--accent:var(--teal)"><h3>Leucemia</h3><p>Alteración de la producción y proliferación de células hematológicas.</p></article>
        <article class="case" style="--accent:var(--gold)"><h3>Trombocitopenia</h3><p>Disminución de plaquetas que puede alterar la hemostasia.</p></article>
        <article class="case" style="--accent:var(--green)"><h3>Hemofilia</h3><p>Alteración de factores de coagulación.</p></article>
        <article class="case" style="--accent:var(--navy2)"><h3>Trombosis</h3><p>Formación patológica de un trombo que puede comprometer el flujo.</p></article>
      </div>
    </section>

    <section class="section" id="bioingenieria">
      <div class="section-head"><div class="chapter"><span class="chapter-num">07</span> De la muestra al dato</div><h2>¿Dónde aparece la ingeniería biomédica?</h2><p class="lead">Una muestra se convierte en señal, la señal en datos y los datos pueden aportar información para una decisión clínica.</p></div>
      <div class="flow" role="img" aria-label="Muestra, sensor, señal, procesamiento y resultado clínico">
        <span class="flow-node red">Muestra</span><span class="flow-arrow">→</span><span class="flow-node teal">Sensor</span><span class="flow-arrow">→</span><span class="flow-node">Señal</span><span class="flow-arrow">→</span><span class="flow-node gold">Procesamiento / IA</span><span class="flow-arrow">→</span><span class="flow-node">Resultado</span>
      </div>
      <div class="tech-map">
        <div class="tech"><strong>Anemia</strong>Hemoglobinómetro</div><div class="tech"><strong>Células sanguíneas</strong>Hematología automatizada</div><div class="tech"><strong>Coagulación</strong>Coagulómetro</div><div class="tech"><strong>Gases</strong>Analizador de gases</div><div class="tech"><strong>Biomarcadores</strong>Biosensores</div><div class="tech"><strong>Células específicas</strong>Citometría de flujo</div><div class="tech"><strong>Trombosis</strong>Ecografía Doppler</div><div class="tech"><strong>Banco de sangre</strong>Conservación y trazabilidad</div>
      </div>
      <div class="two-col" style="margin-top:24px">
        <article class="plain-panel"><h3>La sangre como fuente de datos</h3><p>Una muestra puede aportar hemograma, bioquímica, gases, electrolitos, biomarcadores y otros análisis. Los algoritmos pueden ayudar a reconocer patrones y apoyar la interpretación.</p></article>
        <article class="plain-panel"><h3>Cuando un dispositivo toca sangre</h3><p>Catéteres, stents, válvulas y equipos de diálisis requieren evaluar la respuesta de la sangre.</p><ul class="list" style="--accent:var(--red)"><li>Hemólisis y activación plaquetaria</li><li>Coagulación e inflamación</li><li>Formación de trombos</li></ul></article>
      </div>
      <div class="callout">Reto de diseño: una gota → sensor → datos → alerta útil, portátil y asequible.</div>
    </section>

    <section class="quiz-section" id="preguntas" aria-labelledby="quiz-heading">
      <div class="quiz-intro">
        <div class="quiz-title"><div class="chapter"><span class="chapter-num">08</span> Preguntas al final</div><h2 id="quiz-heading">Reto final: ¿qué aprendiste?</h2><p>Responde antes de abrir la explicación. Puedes usar una pista; luego de elegir, revisa por qué la respuesta tiene sentido.</p></div>
      <div class="quiz-score" aria-live="polite">⭐ <span id="quiz-stars">0</span> estrellas · <span id="quiz-score">0</span> pts · <span id="quiz-progress">0 / 10</span></div>
      </div>
      <div class="quiz-meter" role="progressbar" aria-label="Preguntas contestadas" aria-valuemin="0" aria-valuemax="10" aria-valuenow="0"><span id="quiz-meter-fill"></span></div>
      <div class="questions" id="questions"></div>
    </section>
  </main>
  <footer class="footer"><span>BloodCore · Morfofisiología para Ingeniería Biomédica</span><span>Contenido basado en el resumen de sangre ITM 2026</span></footer>

  <script>
    const quiz = [
      {station:"Componentes",title:"Primera muestra: ¿qué hace el plasma?",prompt:"En el mapa de la sangre, el plasma aparece como la parte líquida. ¿Qué trabajo cumple principalmente?",options:["Transporta nutrientes, hormonas, proteínas y desechos disueltos.","Forma por sí solo el coágulo que detiene una hemorragia.","Es el tipo de leucocito que reconoce microorganismos."],correct:0,hint:"Piensa en el plasma como el medio líquido que lleva sustancias por el cuerpo.",why:"El plasma lleva agua, proteínas, electrolitos, nutrientes, hormonas y productos de desecho."},
      {station:"Componentes",title:"¿Quién ayuda a formar el coágulo?",prompt:"Una muestra muestra que hay pocas plaquetas. ¿Qué función podría verse afectada?",options:["El transporte de oxígeno a los tejidos.","La hemostasia, que ayuda a detener la pérdida de sangre.","La producción de hormonas en el plasma."],correct:1,hint:"Las plaquetas participan cuando un vaso sanguíneo se lesiona.",why:"Las plaquetas se activan y agregan en el sitio de una lesión como parte de la hemostasia."},
      {station:"Hematopoyesis",title:"Sigue el origen de las células",prompt:"¿Dónde se produce continuamente la sangre?",options:["En los alvéolos pulmonares.","En la médula ósea.","En las válvulas del corazón."],correct:1,hint:"Busca el tejido blando que está dentro de ciertos huesos.",why:"La hematopoyesis es la producción de células sanguíneas en la médula ósea."},
      {station:"Hematopoyesis",title:"¿Qué línea da origen a los linfocitos?",prompt:"Los linfocitos T y B participan en la defensa. En el mapa, pertenecen al linaje…",options:["Linfoide.","Mieloide solamente.","Plaquetario."],correct:0,hint:"El esquema separa los linajes mieloide y linfoide.",why:"Los linfocitos T, B y NK aparecen en el linaje linfoide del mapa."},
      {station:"Eritrocitos",title:"El viaje del oxígeno",prompt:"¿Qué molécula del eritrocito se une al oxígeno en los pulmones y lo libera en los tejidos?",options:["Fibrina.","Hemoglobina.","Complemento."],correct:1,hint:"Se mide en un hemograma o con un hemoglobinómetro.",why:"La hemoglobina es la proteína que permite transportar oxígeno en los eritrocitos."},
      {station:"Eritrocitos",title:"Una célula flexible",prompt:"Los vasos pequeños son estrechos. ¿Qué propiedad ayuda al eritrocito a atravesarlos?",options:["Deformabilidad.","Producción de anticuerpos.","Formación de fibrina."],correct:0,hint:"El eritrocito puede cambiar de forma en la microcirculación.",why:"La deformabilidad permite que los eritrocitos pasen por vasos de diámetro pequeño."},
      {station:"Hemostasia",title:"Ordena la respuesta a una lesión",prompt:"¿Qué secuencia describe mejor cómo se forma el coágulo?",options:["Lesión → activación plaquetaria → coagulación → fibrina → coágulo.","Coágulo → lesión → glóbulos rojos → anticuerpos.","Fibrina → oxígeno → lesión → linfocitos."],correct:0,hint:"Las plaquetas se activan antes de que se forme la fibrina.",why:"La secuencia va de la lesión a la activación plaquetaria, coagulación, fibrina, coágulo y reparación."},
      {station:"Bioingeniería",title:"Elige la herramienta",prompt:"Quieres medir gases sanguíneos en una muestra. ¿Qué equipo se relaciona directamente con esa tarea?",options:["Coagulómetro.","Analizador de gases.","Citómetro de flujo."],correct:1,hint:"El nombre del equipo indica qué mide.",why:"El analizador de gases mide variables relacionadas con los gases sanguíneos."},
      {station:"Bioingeniería",title:"¿La sangre y el dispositivo se llevan bien?",prompt:"Un stent va a estar en contacto con la sangre. ¿Qué conviene evaluar?",options:["Solo el color externo del dispositivo.","Hemólisis, activación plaquetaria, coagulación, inflamación y trombosis.","Únicamente la cantidad de glucosa."],correct:1,hint:"Considera si se dañan células o se activa la coagulación.",why:"La biocompatibilidad estudia hemólisis, activación plaquetaria, coagulación, inflamación y formación de trombos."},
      {station:"Bioingeniería",title:"Reto final: diseña para una comunidad rural",prompt:"Tienes una gota de sangre y necesitas una alerta útil en un lugar con pocos recursos. ¿Qué propuesta integra mejor el reto?",options:["Un equipo grande que guarda la muestra y no entrega resultados.","Un dispositivo portátil y económico que detecta un biomarcador, procesa la señal y genera una alerta clara.","Una cámara que toma una foto sin analizarla."],correct:1,hint:"El reto pide una muestra pequeña, un biomarcador, procesamiento, alerta, portabilidad y bajo costo.",why:"La propuesta integra muestra pequeña, biomarcador, procesamiento, alerta, portabilidad y bajo costo."}
    ];
    let score=0, stars=0, answered=0;
    const container=document.getElementById("questions");
    const labels=["A","B","C"];
    quiz.forEach((q,i)=>{
      const article=document.createElement("article"); article.className="question"; article.id=`pregunta-${i+1}`;
      article.innerHTML=`<div class="q-head"><span class="q-num">${String(i+1).padStart(2,"0")}</span><span class="q-station">${q.station}</span></div><h3>${q.title}</h3><p>${q.prompt}</p><div class="answers" role="group" aria-label="Respuestas para la pregunta ${i+1}"></div><div class="q-feedback" aria-live="polite" hidden></div><div class="q-actions"><button class="small-btn" type="button">💡 Ver pista</button><span class="hint" hidden></span></div>`;
      const answers=article.querySelector(".answers"), feedback=article.querySelector(".q-feedback"), hintButton=article.querySelector(".small-btn"), hintText=article.querySelector(".hint");
      let usedHint=false, triedWrong=false, done=false;
      q.options.forEach((option,j)=>{
        const button=document.createElement("button"); button.className="answer"; button.type="button";
        button.innerHTML=`<span class="answer-letter">${labels[j]}</span><span>${option}</span>`;
        button.addEventListener("click",()=>{
          if(done)return;
          if(j!==q.correct){triedWrong=true;button.classList.add("incorrect");button.disabled=true;feedback.hidden=false;feedback.className="q-feedback retry";feedback.innerHTML="<strong>Casi. Intenta otra opción.</strong>Lee de nuevo el mapa de esta sección.";return;}
          done=true;answered++;const points=usedHint||triedWrong?70:100;score+=points;stars++;
          button.classList.add("correct");answers.querySelectorAll("button").forEach(b=>b.disabled=true);
          feedback.hidden=false;feedback.className="q-feedback good";feedback.innerHTML=`<strong>¡Correcto! <span class="star-reward">★ +1 estrella</span> · +${points} puntos</strong>${q.why}`;
          hintButton.disabled=true;updateScore();
        }); answers.appendChild(button);
      });
      hintButton.addEventListener("click",()=>{usedHint=true;hintText.textContent=`Pista: ${q.hint}`;hintText.hidden=false;hintButton.disabled=true;});
      container.appendChild(article);
    });
    function updateScore(){
      document.getElementById("stars-live").textContent=stars;
      document.getElementById("score-live").textContent=score;
      document.getElementById("quiz-stars").textContent=stars;
      document.getElementById("quiz-score").textContent=score;
      document.getElementById("quiz-progress").textContent=`${answered} / ${quiz.length}`;
      document.getElementById("quiz-meter-fill").style.width=`${answered/quiz.length*100}%`;
      document.querySelector(".quiz-meter").setAttribute("aria-valuenow",String(answered));
      ["stars-live","score-live","quiz-stars","quiz-score"].forEach(id=>{const el=document.getElementById(id);el.classList.remove("score-pulse");void el.offsetWidth;el.classList.add("score-pulse")});
    }
    document.getElementById("rotate-model").addEventListener("click",()=>{const cell=document.getElementById("rbc-model");cell.classList.remove("rotate-once");void cell.offsetWidth;cell.classList.add("rotate-once")});
  </script>
</body>
</html>
