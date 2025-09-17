<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>RetroLearn — 1990s Themed eLearning (Demo)</title>
  <style>
    /* ---------- 1990s Retro Web Aesthetic (single-file) ---------- */
    :root{
      --bg1:#0b1020; /* deep blue */
      --neon-pink:#ff3db1;
      --neon-cyan:#00f0ff;
      --neon-yellow:#ffd500;
      --panel:#0f1530;
      --glass: rgba(255,255,255,0.03);
    }
    html,body{height:100%;}
    body{
      margin:0;
      font-family: "Courier New", monospace;
      background:
        radial-gradient(ellipse at 10% 10%, rgba(255,100,200,0.06), transparent 10%),
        radial-gradient(ellipse at 90% 80%, rgba(0,240,255,0.03), transparent 10%),
        linear-gradient(180deg,var(--bg1), #061024 80%);
      color:#e8eefc;
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
      background-attachment:fixed;
    }

    /* subtle scanlines like CRT */
    .scanlines::after{
      content:"";
      position:fixed;
      inset:0;
      pointer-events:none;
      background-image: repeating-linear-gradient(transparent, transparent 3px, rgba(0,0,0,0.05) 4px);
      mix-blend-mode:overlay;
    }

    /* Container */
    .wrap{
      max-width:1100px;
      margin:28px auto;
      padding:18px;
      border:4px solid rgba(255,255,255,0.03);
      background: linear-gradient(180deg, rgba(255,255,255,0.02), rgba(0,0,0,0.04));
      box-shadow: 0 10px 40px rgba(0,0,0,0.6);
      border-radius:8px;
    }

    /* Title bar: neon retro look */
    header{
      display:flex;
      align-items:center;
      gap:14px;
      margin-bottom:18px;
    }
    .logo{
      width:76px;height:76px;
      background:linear-gradient(135deg,var(--neon-pink),var(--neon-cyan));
      border-radius:8px;
      display:grid;place-items:center;
      box-shadow: 0 0 18px rgba(0,255,255,0.06), 0 0 32px rgba(255,61,177,0.06);
      transform:skewX(-6deg);
      font-weight:bold;
      font-size:12px;
      letter-spacing:1px;
    }
    h1{font-size:26px;margin:0;}
    .marquee{
      font-size:11px; color:var(--neon-yellow); margin-left:auto; padding:6px 10px; border-radius:4px;
      background:linear-gradient(90deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
      border:1px dashed rgba(255,255,255,0.03);
    }

    /* Search and nav */
    .topbar{display:flex;gap:12px;align-items:center;margin-bottom:14px}
    .search{
      flex:1; display:flex; gap:8px; align-items:center;
    }
    .search input{
      flex:1; padding:10px 12px; border-radius:6px; border:2px solid rgba(255,255,255,0.06);
      background:linear-gradient(180deg, rgba(255,255,255,0.01), rgba(0,0,0,0.03));
      outline:none; font-family:inherit; color:inherit;
    }
    .btn{
      padding:10px 14px; border-radius:6px; cursor:pointer; font-weight:bold;
      border:2px solid rgba(255,255,255,0.06); background:var(--glass);
      box-shadow: 0 6px 12px rgba(0,0,0,0.5);
    }

    /* Layout: sidebar + main */
    .layout{display:flex; gap:16px}
    aside{
      width:260px; padding:12px; border-radius:6px; background:linear-gradient(180deg, rgba(255,255,255,0.01), rgba(0,0,0,0.03));
      border:1px solid rgba(255,255,255,0.02);
    }
    main{flex:1;padding:12px;}

    /* Retro menu items */
    .menu a{display:block;padding:8px;border-radius:4px;margin-bottom:6px;text-decoration:none;color:inherit}
    .menu a:hover{background:rgba(255,255,255,0.02);}

    /* Course grid styled as 90s boxed cards */
    .courses{display:grid;grid-template-columns:repeat(auto-fill,minmax(220px,1fr));gap:12px}
    .card{
      padding:10px;border-radius:6px;border:3px inset rgba(0,0,0,0.6); background:linear-gradient(180deg, rgba(255,255,255,0.01), rgba(0,0,0,0.06));
      box-shadow: 0 6px 18px rgba(0,0,0,0.6);
    }
    .card h3{margin:6px 0 4px;font-size:14px}
    .card p{margin:0;font-size:12px;opacity:0.9}

    /* Neon badge */
    .badge{display:inline-block;padding:6px 8px;border-radius:6px;font-weight:bold;font-size:11px;margin-top:8px}
    .badge.new{background:linear-gradient(90deg,var(--neon-pink),var(--neon-cyan));color:#051225}

    /* 90s CRT glow effect on hover */
    .card:hover{transform:translateY(-4px);transition:transform .18s ease; box-shadow:0 12px 28px rgba(0,0,0,0.7), 0 0 18px rgba(0,240,255,0.06);}

    /* pixel-ish button */
    .pixel-btn{
      display:inline-block;padding:10px 12px;text-transform:uppercase;border:3px solid #000;background:linear-gradient(180deg,#fff,#ddd);font-weight:bold; font-size:12px; border-radius:3px;
      box-shadow: 3px 3px 0 rgba(0,0,0,0.6);
      margin-top:8px;
    }

    /* footer */
    footer{margin-top:18px;font-size:12px;opacity:0.8}

    /* tiny retro icons with ASCII look */
    .ascii{font-family:monospace;font-size:11px;color:var(--neon-cyan)}

    /* Responsive tweaks */
    @media (max-width:720px){
      aside{display:none}
      .wrap{margin:10px}
      .logo{width:56px;height:56px}
    }

    /* Extra : animated scanline shimmer */
    .vhs::before{
      content:"";position:absolute;left:-50%;top:0;width:50%;height:100%;background:linear-gradient(90deg, rgba(255,255,255,0.03), rgba(255,255,255,0.12), rgba(255,255,255,0.03));transform:skewX(-20deg);opacity:0.02;animation:shimmer 6s linear infinite;
    }
    @keyframes shimmer{from{left:-50%}to{left:150%}}

    /* simple pixel border for a strong 90s boxed aesthetic */
    .pixel-border{border:6px solid #000; padding:6px; background:linear-gradient(180deg,#0d1828,#061024)}

  </style>
</head>
<body class="scanlines">
  <div class="wrap vhs pixel-border">
    <header>
      <div class="logo">Retro
        <div style="font-size:10px;opacity:0.9;line-height:10px">Learn</div>
      </div>
      <h1>RetroLearn — Courses in 1990s Style</h1>
      <div class="marquee"><marquee behavior="scroll" direction="left" scrollamount="6">NEW: Web Design Basics • C Programming • Pixel Art • '90s Web Culture — Enroll now!</marquee></div>
    </header>

    <div class="topbar">
      <div class="search">
        <input id="q" placeholder="Search courses (try: 'C Programming')" />
        <button class="btn" onclick="search()">Search</button>
      </div>
      <div style="display:flex;gap:8px">
        <button class="btn" onclick="toggleTheme()">Toggle Neon</button>
        <button class="btn" onclick="preview()">Preview</button>
      </div>
    </div>

    <div class="layout">
      <aside>
        <div style="font-size:13px;font-weight:bold;margin-bottom:8px">Menu</div>
        <nav class="menu">
          <a href="#">Home</a>
          <a href="#">All Courses</a>
          <a href="#">My Learning</a>
          <a href="#">Profile</a>
          <a href="#">Support</a>
        </nav>

        <hr style="opacity:0.06;margin:10px 0">
        <div style="font-size:13px;font-weight:bold;margin-bottom:6px">Categories</div>
        <div class="ascii">[1] Programming<br>[2] Design<br>[3] Arts<br>[4] Business</div>
      </aside>

      <main>
        <section style="margin-bottom:12px">
          <div style="display:flex;justify-content:space-between;align-items:center">
            <div style="font-size:15px;font-weight:bold">Featured Courses</div>
            <div style="font-size:12px;opacity:0.9">Showing <span id="count">6</span> courses</div>
          </div>
        </section>

        <section class="courses" id="courses">
          <!-- Course Card Template: JS will render some sample items -->
        </section>

        <footer>
          <div>© RetroLearn 1997 — This is a demo UI inspired by 1990s web aesthetics. For production, connect to a modern backend and replace <code>&lt;marquee&gt;</code> if desired.</div>
        </footer>
      </main>
    </div>
  </div>

  <script>
    // Sample data (mock courses)
    const sample = [
      {title:'C Programming: From Scratch', author:'Prof. A. Rao', desc:'Basics to advanced C.', tag:'new'},
      {title:'Pixel Art for Beginners', author:'S. Kapoor', desc:'Make 16x16 sprites.', tag:''},
      {title:'HTML & CSS — 1997 Edition', author:'Retro Web Team', desc:'Build websites like it\'s 1997.', tag:'new'},
      {title:'Data Structures (Intro)', author:'Dr. Nair', desc:'Arrays, lists and trees.', tag:''},
      {title:'Digital Logic', author:'E. Iyer', desc:'Gates and circuits.', tag:''},
      {title:'Introduction to Photography', author:'L. Mehta', desc:'Film techniques & composition.', tag:''}
    ];

    function render(list){
      const el = document.getElementById('courses'); el.innerHTML='';
      list.forEach(c=>{
        const card = document.createElement('div'); card.className='card';
        card.innerHTML = `<div style=\"display:flex;justify-content:space-between;align-items:center\">`+
                         `<div style=\"font-size:11px;opacity:0.8\">${c.author}</div>`+
                         `${c.tag?'<div class="badge new">NEW</div>':''}`+
                         `</div>`+
                         `<h3>${c.title}</h3>`+
                         `<p>${c.desc}</p>`+
                         `<div><a class=\"pixel-btn\" href=\"#\">Enroll</a></div>`;
        el.appendChild(card);
      });
      document.getElementById('count').textContent = list.length;
    }

    render(sample);

    function search(){
      const q = document.getElementById('q').value.trim().toLowerCase();
      if(!q) return render(sample);
      const filtered = sample.filter(s => (s.title + ' ' + s.desc + ' ' + s.author).toLowerCase().includes(q));
      render(filtered);
    }

    // Neon toggle (tints the UI)
    let neon=false;
    function toggleTheme(){
      neon = !neon;
      if(neon){
        document.documentElement.style.setProperty('--bg1','#071028');
        document.documentElement.style.setProperty('--neon-pink','#ff7bd1');
        document.documentElement.style.setProperty('--neon-cyan','#00f0ff');
      } else {
        document.documentElement.style.setProperty('--bg1','#0b1020');
        document.documentElement.style.setProperty('--neon-pink','#ff3db1');
        document.documentElement.style.setProperty('--neon-cyan','#00f0ff');
      }
    }

    function preview(){
      alert('This is a static demo page. To turn it into a real app: add a backend (Node/Python), user accounts, and a course database.');
    }
  </script>
</body>
</html>
