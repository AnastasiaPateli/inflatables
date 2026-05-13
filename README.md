<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Inflatable Structure</title>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&family=DM+Mono:wght@300;400&display=swap" rel="stylesheet" />

  <style>
    /* ─── Reset & Base ─────────────────────────────────────────── */
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --bg:        #0d0d0b;
      --surface:   #131310;
      --border:    rgba(255,255,255,0.08);
      --text:      #e8e4dc;
      --muted:     #7a7568;
      --accent:    #c8b98a;
      --accent2:   #8fb3a0;
      --ff-serif:  'Cormorant Garamond', Georgia, serif;
      --ff-mono:   'DM Mono', monospace;
    }

    html { scroll-behavior: smooth; }

    body {
      background: var(--bg);
      color: var(--text);
      font-family: var(--ff-serif);
      font-size: 18px;
      line-height: 1.75;
      overflow-x: hidden;
    }

    ::selection { background: var(--accent); color: var(--bg); }

    /* ─── Scrollbar ─────────────────────────────────────────────── */
    ::-webkit-scrollbar { width: 4px; }
    ::-webkit-scrollbar-track { background: var(--bg); }
    ::-webkit-scrollbar-thumb { background: var(--accent); border-radius: 2px; }

    /* ─── Hero ──────────────────────────────────────────────────── */
    #hero {
      height: 100svh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      text-align: center;
      position: relative;
      overflow: hidden;
    }

    /* subtle animated grain */
    #hero::before {
      content: '';
      position: absolute;
      inset: -50%;
      width: 200%; height: 200%;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.06'/%3E%3C/svg%3E");
      opacity: 0.5;
      animation: drift 12s ease-in-out infinite alternate;
      pointer-events: none;
    }

    @keyframes drift {
      from { transform: translate(0, 0); }
      to   { transform: translate(2%, 2%); }
    }

    /* radial glow behind title */
    #hero::after {
      content: '';
      position: absolute;
      width: 600px; height: 600px;
      background: radial-gradient(circle, rgba(200,185,138,0.07) 0%, transparent 70%);
      top: 50%; left: 50%;
      transform: translate(-50%, -50%);
      pointer-events: none;
    }

    .hero-eyebrow {
      font-family: var(--ff-mono);
      font-size: 0.7rem;
      letter-spacing: 0.25em;
      color: var(--accent);
      text-transform: uppercase;
      margin-bottom: 2rem;
      opacity: 0;
      animation: fadeUp 1s 0.3s forwards;
    }

    .hero-title {
      font-size: clamp(3.5rem, 10vw, 8rem);
      font-weight: 300;
      letter-spacing: -0.01em;
      line-height: 1.05;
      color: var(--text);
      opacity: 0;
      animation: fadeUp 1s 0.6s forwards;
    }

    .hero-title em {
      font-style: italic;
      color: var(--accent);
    }

    .hero-sub {
      margin-top: 2rem;
      font-family: var(--ff-mono);
      font-size: 0.75rem;
      color: var(--muted);
      letter-spacing: 0.15em;
      opacity: 0;
      animation: fadeUp 1s 0.9s forwards;
    }

    .hero-scroll {
      position: absolute;
      bottom: 2.5rem;
      left: 50%;
      transform: translateX(-50%);
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 0.5rem;
      opacity: 0;
      animation: fadeUp 1s 1.4s forwards;
    }

    .hero-scroll span {
      font-family: var(--ff-mono);
      font-size: 0.6rem;
      letter-spacing: 0.2em;
      color: var(--muted);
      text-transform: uppercase;
    }

    .scroll-line {
      width: 1px; height: 40px;
      background: linear-gradient(to bottom, var(--accent), transparent);
      animation: scrollPulse 2s ease-in-out infinite;
    }

    @keyframes scrollPulse {
      0%, 100% { opacity: 0.3; transform: scaleY(1); }
      50%       { opacity: 1;   transform: scaleY(1.2); }
    }

    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(24px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    /* ─── Nav ───────────────────────────────────────────────────── */
    nav {
      position: fixed;
      top: 0; left: 0; right: 0;
      z-index: 100;
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 1.25rem 3rem;
      background: linear-gradient(to bottom, rgba(13,13,11,0.95), transparent);
      backdrop-filter: blur(4px);
      transition: background 0.4s;
    }

    .nav-logo {
      font-family: var(--ff-mono);
      font-size: 0.65rem;
      letter-spacing: 0.18em;
      color: var(--accent);
      text-transform: uppercase;
      text-decoration: none;
    }

    .nav-links {
      display: flex;
      gap: 2rem;
      list-style: none;
    }

    .nav-links a {
      font-family: var(--ff-mono);
      font-size: 0.65rem;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      color: var(--muted);
      text-decoration: none;
      transition: color 0.2s;
    }

    .nav-links a:hover { color: var(--accent); }

    /* ─── Sections Layout ───────────────────────────────────────── */
    main { max-width: 1200px; margin: 0 auto; padding: 0 2rem; }

    section {
      padding: 8rem 0;
      border-top: 1px solid var(--border);
      opacity: 0;
      transform: translateY(40px);
      transition: opacity 0.8s ease, transform 0.8s ease;
    }

    section.visible {
      opacity: 1;
      transform: translateY(0);
    }

    .section-label {
      font-family: var(--ff-mono);
      font-size: 0.65rem;
      letter-spacing: 0.25em;
      color: var(--accent);
      text-transform: uppercase;
      margin-bottom: 1.5rem;
      display: flex;
      align-items: center;
      gap: 1rem;
    }

    .section-label::after {
      content: '';
      flex: 1;
      height: 1px;
      background: var(--border);
      max-width: 80px;
    }

    h2 {
      font-size: clamp(2rem, 5vw, 3.5rem);
      font-weight: 300;
      line-height: 1.1;
      margin-bottom: 2.5rem;
      color: var(--text);
    }

    h2 em { font-style: italic; color: var(--accent); }

    h3 {
      font-size: 1.4rem;
      font-weight: 400;
      margin-bottom: 1rem;
      margin-top: 3rem;
      color: var(--text);
    }

    p { color: rgba(232,228,220,0.75); margin-bottom: 1.25rem; max-width: 68ch; }

    /* ─── Two-column layout ─────────────────────────────────────── */
    .two-col {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 4rem;
      align-items: start;
    }

    @media (max-width: 768px) {
      .two-col { grid-template-columns: 1fr; gap: 2rem; }
      nav { padding: 1rem 1.5rem; }
      .nav-links { display: none; }
      main { padding: 0 1.25rem; }
      section { padding: 5rem 0; }
    }

    /* ─── Image placeholders / real images ─────────────────────── */
    .img-wrap {
      width: 100%;
      aspect-ratio: 4/3;
      background: var(--surface);
      border: 1px solid var(--border);
      overflow: hidden;
      position: relative;
    }

    .img-wrap img {
      width: 100%; height: 100%;
      object-fit: cover;
      display: block;
      transition: transform 0.6s ease;
    }

    .img-wrap:hover img { transform: scale(1.04); }

    /* placeholder when no image */
    .img-placeholder {
      position: absolute;
      inset: 0;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      gap: 0.5rem;
      color: var(--muted);
    }

    .img-placeholder .icon { font-size: 2rem; opacity: 0.3; }

    .img-placeholder span {
      font-family: var(--ff-mono);
      font-size: 0.6rem;
      letter-spacing: 0.15em;
      text-transform: uppercase;
    }

    .img-caption {
      font-family: var(--ff-mono);
      font-size: 0.65rem;
      color: var(--muted);
      margin-top: 0.75rem;
      letter-spacing: 0.1em;
    }

    /* ─── Process Steps ─────────────────────────────────────────── */
    .steps {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
      gap: 2px;
      margin-top: 3rem;
    }

    .step {
      background: var(--surface);
      padding: 2rem;
      border: 1px solid var(--border);
      transition: background 0.3s;
    }

    .step:hover { background: rgba(200,185,138,0.04); }

    .step-num {
      font-family: var(--ff-mono);
      font-size: 0.6rem;
      letter-spacing: 0.2em;
      color: var(--accent);
      margin-bottom: 1rem;
    }

    .step h4 {
      font-size: 1.1rem;
      font-weight: 400;
      margin-bottom: 0.75rem;
      color: var(--text);
    }

    .step p { font-size: 0.9rem; max-width: none; }

    /* ─── Gallery ───────────────────────────────────────────────── */
    .gallery {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 2px;
      margin-top: 3rem;
    }

    @media (max-width: 600px) { .gallery { grid-template-columns: repeat(2, 1fr); } }

    .gallery-item {
      aspect-ratio: 1;
      background: var(--surface);
      overflow: hidden;
      cursor: pointer;
      position: relative;
    }

    .gallery-item img {
      width: 100%; height: 100%;
      object-fit: cover;
      display: block;
      transition: transform 0.5s ease, opacity 0.3s;
      opacity: 0.85;
    }

    .gallery-item:hover img { transform: scale(1.06); opacity: 1; }

    /* placeholder for gallery */
    .gallery-ph {
      position: absolute;
      inset: 0;
      display: flex;
      align-items: center;
      justify-content: center;
      font-family: var(--ff-mono);
      font-size: 0.6rem;
      color: var(--muted);
      letter-spacing: 0.1em;
    }

    /* ─── Inspiration quote ─────────────────────────────────────── */
    blockquote {
      border-left: 2px solid var(--accent);
      padding: 1.5rem 2rem;
      margin: 3rem 0;
      background: var(--surface);
      font-style: italic;
      font-size: 1.05rem;
      color: rgba(232,228,220,0.8);
    }

    blockquote cite {
      display: block;
      margin-top: 1rem;
      font-style: normal;
      font-family: var(--ff-mono);
      font-size: 0.65rem;
      color: var(--accent);
      letter-spacing: 0.1em;
    }

    /* ─── Bibliography ──────────────────────────────────────────── */
    .bib-list {
      list-style: none;
      margin-top: 2rem;
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 0.5rem 3rem;
    }

    @media (max-width: 700px) { .bib-list { grid-template-columns: 1fr; } }

    .bib-list li {
      font-family: var(--ff-mono);
      font-size: 0.72rem;
      color: var(--muted);
      padding: 0.4rem 0;
      border-bottom: 1px solid var(--border);
      transition: color 0.2s;
    }

    .bib-list li:hover { color: var(--accent); }

    .bib-list a { color: inherit; text-decoration: none; }

    /* ─── Team ──────────────────────────────────────────────────── */
    .team-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
      gap: 2rem;
      margin-top: 3rem;
    }

    .team-card {
      text-align: center;
    }

    .avatar {
      width: 72px; height: 72px;
      border-radius: 50%;
      background: var(--surface);
      border: 1px solid var(--border);
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 1.1rem;
      font-weight: 300;
      color: var(--accent);
      margin: 0 auto 1rem;
      letter-spacing: 0.04em;
      font-family: var(--ff-serif);
    }

    .team-card .name {
      font-size: 0.95rem;
      font-weight: 400;
      color: var(--text);
      line-height: 1.3;
    }

    .team-card .role {
      font-family: var(--ff-mono);
      font-size: 0.6rem;
      color: var(--muted);
      letter-spacing: 0.12em;
      text-transform: uppercase;
      margin-top: 0.3rem;
    }

    .team-card a {
      font-family: var(--ff-mono);
      font-size: 0.6rem;
      color: var(--accent2);
      text-decoration: none;
      display: block;
      margin-top: 0.2rem;
    }

    /* professors separator */
    .divider-label {
      font-family: var(--ff-mono);
      font-size: 0.65rem;
      letter-spacing: 0.2em;
      color: var(--muted);
      text-transform: uppercase;
      margin: 4rem 0 1rem;
      display: flex;
      align-items: center;
      gap: 1rem;
    }

    .divider-label::before, .divider-label::after {
      content: '';
      flex: 1;
      height: 1px;
      background: var(--border);
    }

    /* ─── Footer ────────────────────────────────────────────────── */
    footer {
      border-top: 1px solid var(--border);
      text-align: center;
      padding: 3rem 2rem;
      font-family: var(--ff-mono);
      font-size: 0.65rem;
      color: var(--muted);
      letter-spacing: 0.12em;
    }

    /* ─── Lightbox ──────────────────────────────────────────────── */
    #lightbox {
      display: none;
      position: fixed;
      inset: 0;
      background: rgba(0,0,0,0.92);
      z-index: 999;
      align-items: center;
      justify-content: center;
      padding: 2rem;
    }

    #lightbox.open { display: flex; }

    #lightbox img {
      max-width: 90vw;
      max-height: 85vh;
      object-fit: contain;
      border: 1px solid var(--border);
    }

    #lightbox-close {
      position: absolute;
      top: 1.5rem; right: 2rem;
      background: none; border: none;
      color: var(--muted);
      font-size: 1.5rem;
      cursor: pointer;
      font-family: var(--ff-mono);
      transition: color 0.2s;
    }

    #lightbox-close:hover { color: var(--accent); }

    /* ─── Ordered list styling ───────────────────────────────────── */
    ol {
      padding-left: 1.5rem;
      color: rgba(232,228,220,0.75);
      display: flex;
      flex-direction: column;
      gap: 0.5rem;
    }

    ol li { font-size: 0.95rem; }

    /* ─── Tag chips ─────────────────────────────────────────────── */
    .tags { display: flex; flex-wrap: wrap; gap: 0.5rem; margin-top: 1.5rem; }

    .tag {
      font-family: var(--ff-mono);
      font-size: 0.6rem;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      padding: 0.3rem 0.8rem;
      border: 1px solid var(--border);
      color: var(--muted);
      border-radius: 999px;
    }
  </style>
</head>

<body>

  <!-- ─── Navigation ─────────────────────────────────────────── -->
  <nav>
    <a href="#hero" class="nav-logo">Inflatable Structure</a>
    <ul class="nav-links">
      <li><a href="#idea">Concept</a></li>
      <li><a href="#process">Process</a></li>
      <li><a href="#simulation">Simulation</a></li>
      <li><a href="#construction">Construction</a></li>
      <li><a href="#gallery">Gallery</a></li>
      <li><a href="#team">Team</a></li>
    </ul>
  </nav>

  <!-- ─── Hero ───────────────────────────────────────────────── -->
  <section id="hero" style="border:none; opacity:1; transform:none; padding:0;">
    <p class="hero-eyebrow">Geometrical &amp; Digital Representations — Applied Architectural Design</p>
    <h1 class="hero-title"><em>Inflatable</em><br>Structure</h1>
    <p class="hero-sub">4th Semester · Spring 2025 &nbsp;·&nbsp; [Your University Name]</p>
    <div class="hero-scroll">
      <span>Scroll</span>
      <div class="scroll-line"></div>
    </div>
  </section>

  <main>

    <!-- ─── Cover Image ──────────────────────────────────────── -->
    <section id="cover" style="padding-top: 2rem; padding-bottom: 5rem;">
      <div class="img-wrap" style="aspect-ratio: 16/7;">
        <!-- Replace src with your hero/final model image -->
        <img src="images/cover.jpg" alt="Final inflatable structure" onerror="this.style.display='none'" />
        <div class="img-placeholder">
          <span class="icon">◻</span>
          <span>Replace with your final model photo</span>
        </div>
      </div>
      <p class="img-caption">// Final model — Scale 1:1</p>
    </section>

    <!-- ─── Idea ─────────────────────────────────────────────── -->
    <section id="idea">
      <div class="section-label">01 — Concept</div>
      <div class="two-col">
        <div>
          <h2>The <em>Idea</em></h2>
          <p>
            Our research problem emerged from the desire to give meaningful form to air. We explored how simple
            digital simulations of inflatables could generate panel geometries that, when fabricated and joined,
            assemble into a coherent, buildable structure.
          </p>
          <p>
            The starting point was a custom boundary curve drawn freely in Rhino — the rest of the workflow
            was designed to be fully parametric, allowing rapid iteration between design intent and physical output.
          </p>
          <div class="tags">
            <span class="tag">Grasshopper 3D</span>
            <span class="tag">Rhino</span>
            <span class="tag">Kangaroo2</span>
            <span class="tag">Parametric Design</span>
            <span class="tag">Developable Surfaces</span>
          </div>
        </div>
        <div>
          <div class="img-wrap">
            <img src="images/design/idea.jpg" alt="Initial concept sketches" onerror="this.style.display='none'" />
            <div class="img-placeholder"><span class="icon">◻</span><span>Concept sketch / initial curves</span></div>
          </div>
          <p class="img-caption">// Input curves in Rhino</p>
        </div>
      </div>
    </section>

    <!-- ─── Process ──────────────────────────────────────────── -->
    <section id="process">
      <div class="section-label">02 — Process</div>
      <h2>Design <em>Process</em></h2>
      <p>From boundary curve to unrolled fabrication panels — a fully parametric pipeline built in Grasshopper.</p>

      <div class="steps">
        <div class="step">
          <div class="step-num">Step 01</div>
          <h4>First Sketches</h4>
          <p>Initial hand sketches explored the possible forms our inflatable structure could take and methods for transforming arbitrary shapes into buildable structures.</p>
        </div>
        <div class="step">
          <div class="step-num">Step 02</div>
          <h4>Grasshopper Setup</h4>
          <p>We began the digital workflow by inputting the component curves into Grasshopper. Creating a suitable mesh was the first challenge — triangulate and quad mesh components were tested before finding the right approach.</p>
        </div>
        <div class="step">
          <div class="step-num">Step 03</div>
          <h4>Skeleton Line &amp; Grid</h4>
          <p>After exploring offset, tween curve, and Voronoi approaches, we used the <em>Medial Axis from Region</em> tool (Nautilus plugin) to extract a clean, continuous skeleton line and build our panel grid.</p>
        </div>
        <div class="step">
          <div class="step-num">Step 04</div>
          <h4>Lists &amp; Final Grid</h4>
          <p>Using Flip Matrix, Shift List, Partition List and Explode Tree, we organised the grid strips into separate component curves and generated the transverse strips using Pull Point to Curve and Polyline.</p>
        </div>
      </div>

      <div class="two-col" style="margin-top: 4rem;">
        <div>
          <div class="img-wrap">
            <img src="images/design/grid.jpg" alt="Grid development" onerror="this.style.display='none'" />
            <div class="img-placeholder"><span class="icon">◻</span><span>Skeleton line & grid</span></div>
          </div>
          <p class="img-caption">// Medial axis and panel grid</p>
        </div>
        <div>
          <div class="img-wrap">
            <img src="images/design/panels.jpg" alt="Unrolled panels" onerror="this.style.display='none'" />
            <div class="img-placeholder"><span class="icon">◻</span><span>Unrolled panels / pattern</span></div>
          </div>
          <p class="img-caption">// Unrolled fabrication pieces</p>
        </div>
      </div>
    </section>

    <!-- ─── Simulation ────────────────────────────────────────── -->
    <section id="simulation">
      <div class="section-label">03 — Simulation</div>
      <div class="two-col">
        <div>
          <h2>Kangaroo <em>Simulation</em></h2>
          <p>
            With the geometry defined, we used Kangaroo 2 to simulate the pneumatic behaviour of the structure
            under internal pressure. The simulation allowed us to study how the surface deforms and to verify
            that our panels would produce the intended inflated form.
          </p>
          <h3>Steps</h3>
          <ol>
            <li>Input the boundary surface into the Grasshopper file.</li>
            <li>Triangulate the mesh for more realistic material behaviour.</li>
            <li>Apply internal pressure and anchor the required boundary points.</li>
            <li>Activate the Kangaroo Solver.</li>
            <li>Adjust the pressure slider to observe the structure under different load conditions.</li>
          </ol>
        </div>
        <div>
          <div class="img-wrap" style="aspect-ratio: 3/4;">
            <img src="images/design/simulation.jpg" alt="Kangaroo simulation" onerror="this.style.display='none'" />
            <div class="img-placeholder"><span class="icon">◻</span><span>Kangaroo simulation screenshot</span></div>
          </div>
          <p class="img-caption">// Inflated mesh — Kangaroo 2</p>
        </div>
      </div>

      <h3 style="margin-top: 4rem;">Developable Surfaces Methodology</h3>
      <p>To produce fabricable flat panels from the inflated mesh, we followed this methodology:</p>
      <ol>
        <li>Extrude medial axis grid lines along the Z axis to a suitable height.</li>
        <li>Convert extruded surfaces from Brep to mesh.</li>
        <li>Split the inflated mesh using the extruded surfaces (Mesh Split component).</li>
        <li>Find the naked edges of each sub-mesh to obtain its boundary.</li>
        <li>Close open boundaries using Join Curves / Close Curve as needed.</li>
        <li>Reconstruct each panel with Mesh Patch.</li>
        <li>Bake, convert to NURBS, and Unroll for fabrication.</li>
      </ol>
    </section>

    <!-- ─── Construction ─────────────────────────────────────── -->
    <section id="construction">
      <div class="section-label">04 — Construction</div>
      <h2>Model <em>Construction</em></h2>
      <p style="font-family: var(--ff-mono); font-size: 0.7rem; color: var(--accent); letter-spacing: 0.1em;">Scale 1:1 · Material: [Your material here]</p>

      <div class="two-col" style="margin-top: 3rem;">
        <div>
          <h3>Material &amp; Zoning</h3>
          <p>
            The structure was divided into [X] major zones based on the cylindrical regions recognisable in the
            Rhino file. Each zone corresponds to a distinct area of the inflated surface and was cut and joined separately
            before being assembled into the complete form.
          </p>
          <p>
            Replace this text with details about your material choice, roll dimensions, and how you grouped
            the panels for fabrication.
          </p>
        </div>
        <div>
          <h3>Grid Marking</h3>
          <p>
            The material roll was laid out in an open space and a 0.5 m × 0.5 m reference grid was marked using
            [your method: cardboard templates, floor tiles, laser device, etc.]. Panel outlines were drawn by hand,
            locating key points on the grid and connecting them with straight lines.
          </p>
          <p>
            Replace this with the specifics of your marking and cutting process.
          </p>
        </div>
      </div>

      <div class="steps" style="margin-top: 3rem;">
        <div class="step">
          <div class="step-num">Phase 01</div>
          <h4>Grouping &amp; Zoning</h4>
          <p>All pieces were catalogued and grouped into zones to manage the cutting and joining sequence systematically.</p>
        </div>
        <div class="step">
          <div class="step-num">Phase 02</div>
          <h4>Grid Marking</h4>
          <p>A reference grid was set up on the material. Key points for each panel were located on the grid and marked.</p>
        </div>
        <div class="step">
          <div class="step-num">Phase 03</div>
          <h4>Drawing &amp; Tabs</h4>
          <p>Panel outlines were drawn and 15 cm seam tabs were added on each side to allow joining without distortion.</p>
        </div>
        <div class="step">
          <div class="step-num">Phase 04</div>
          <h4>Cutting &amp; Joining</h4>
          <p>All pieces on each sheet were drawn before cutting began. Panels were joined using [your joining method, e.g. heat sealing / iron / sewing].</p>
        </div>
      </div>

      <div class="img-wrap" style="margin-top: 3rem; aspect-ratio: 16/7;">
        <img src="images/construction.jpg" alt="Construction process" onerror="this.style.display='none'" />
        <div class="img-placeholder"><span class="icon">◻</span><span>Construction process photo</span></div>
      </div>
      <p class="img-caption">// Marking and cutting at [location]</p>
    </section>

    <!-- ─── Gallery ──────────────────────────────────────────── -->
    <section id="gallery">
      <div class="section-label">05 — Gallery</div>
      <h2>Photo <em>Gallery</em></h2>
      <p>Replace the <code>src</code> attributes below with paths to your own images. Add or remove <code>.gallery-item</code> divs as needed.</p>

      <div class="gallery">
        <!-- Add your images here. Pattern: <div class="gallery-item"><img src="images/photo01.jpg" alt="..." /></div> -->
        <!-- Placeholder tiles shown when no image src is set -->
        <div class="gallery-item"><img src="images/gallery/01.jpg" alt="Photo 1" onerror="this.style.display='none'" /><div class="gallery-ph">01</div></div>
        <div class="gallery-item"><img src="images/gallery/02.jpg" alt="Photo 2" onerror="this.style.display='none'" /><div class="gallery-ph">02</div></div>
        <div class="gallery-item"><img src="images/gallery/03.jpg" alt="Photo 3" onerror="this.style.display='none'" /><div class="gallery-ph">03</div></div>
        <div class="gallery-item"><img src="images/gallery/04.jpg" alt="Photo 4" onerror="this.style.display='none'" /><div class="gallery-ph">04</div></div>
        <div class="gallery-item"><img src="images/gallery/05.jpg" alt="Photo 5" onerror="this.style.display='none'" /><div class="gallery-ph">05</div></div>
        <div class="gallery-item"><img src="images/gallery/06.jpg" alt="Photo 6" onerror="this.style.display='none'" /><div class="gallery-ph">06</div></div>
        <div class="gallery-item"><img src="images/gallery/07.jpg" alt="Photo 7" onerror="this.style.display='none'" /><div class="gallery-ph">07</div></div>
        <div class="gallery-item"><img src="images/gallery/08.jpg" alt="Photo 8" onerror="this.style.display='none'" /><div class="gallery-ph">08</div></div>
        <div class="gallery-item"><img src="images/gallery/09.jpg" alt="Photo 9" onerror="this.style.display='none'" /><div class="gallery-ph">09</div></div>
      </div>
    </section>

    <!-- ─── Inspiration ───────────────────────────────────────── -->
    <section id="inspiration">
      <div class="section-label">06 — Inspiration</div>
      <h2><em>Inspiration</em> &amp; References</h2>
      <p>
        Our project was inspired by [Name / Project], who explored [brief description of the inspiring project or idea].
        Their methodology of [key method] gave us a strong conceptual foundation and we are grateful for the tips and
        encouragement they shared with us.
      </p>

      <blockquote>
        "Replace this with a real quote from your inspiration source, collaborator, or professor that shaped the direction
        of your project. Even a short sentence can be powerful here."
        <cite>— [Name, role / affiliation]</cite>
      </blockquote>

      <div class="two-col" style="margin-top: 2rem;">
        <div>
          <div class="img-wrap">
            <img src="images/inspiration/ref1.jpg" alt="Reference project" onerror="this.style.display='none'" />
            <div class="img-placeholder"><span class="icon">◻</span><span>Reference project image</span></div>
          </div>
          <p class="img-caption">// [Reference project name]</p>
        </div>
        <div>
          <div class="img-wrap">
            <img src="images/inspiration/ref2.jpg" alt="Reference project" onerror="this.style.display='none'" />
            <div class="img-placeholder"><span class="icon">◻</span><span>Reference project image</span></div>
          </div>
          <p class="img-caption">// [Reference project methodology]</p>
        </div>
      </div>
    </section>

    <!-- ─── Bibliography ─────────────────────────────────────── -->
    <section id="bibliography">
      <div class="section-label">07 — Bibliography</div>
      <h2><em>Bibliography</em></h2>

      <p style="font-family: var(--ff-mono); font-size: 0.7rem; color: var(--muted);">Websites</p>
      <ul class="bib-list">
        <li><a href="#">Grasshopper 3D — grasshopper3d.com</a></li>
        <li><a href="#">McNeel Discourse — discourse.mcneel.com</a></li>
        <li><a href="#">Kangaroo Physics — food4rhino.com</a></li>
        <li><a href="#">Grasshopper Docs — grasshopperdocs.com</a></li>
        <li><a href="#">[Add your source] — source.com</a></li>
        <li><a href="#">[Add your source] — source.com</a></li>
      </ul>

      <p style="font-family: var(--ff-mono); font-size: 0.7rem; color: var(--muted); margin-top: 2rem;">Books &amp; Papers</p>
      <ul class="bib-list">
        <li>Advances in Architectural Geometry 2014–2023</li>
        <li>[Author, A. — Book Title, Year]</li>
        <li>[Author, B. — Paper Title, Journal, Year]</li>
        <li>[Add your reference here]</li>
      </ul>
    </section>

    <!-- ─── Team ──────────────────────────────────────────────── -->
    <section id="team">
      <div class="section-label">08 — People</div>
      <h2>The <em>Team</em></h2>

      <div class="team-grid">
        <!-- Students — replace initials, names, and Instagram handles -->
        <div class="team-card">
          <div class="avatar">AB</div>
          <div class="name">Firstname<br>Lastname</div>
          <div class="role">Student</div>
          <a href="https://instagram.com/" target="_blank">@handle</a>
        </div>
        <div class="team-card">
          <div class="avatar">CD</div>
          <div class="name">Firstname<br>Lastname</div>
          <div class="role">Student</div>
          <a href="https://instagram.com/" target="_blank">@handle</a>
        </div>
        <div class="team-card">
          <div class="avatar">EF</div>
          <div class="name">Firstname<br>Lastname</div>
          <div class="role">Student</div>
          <a href="https://instagram.com/" target="_blank">@handle</a>
        </div>
        <div class="team-card">
          <div class="avatar">GH</div>
          <div class="name">Firstname<br>Lastname</div>
          <div class="role">Student</div>
          <a href="https://instagram.com/" target="_blank">@handle</a>
        </div>
        <div class="team-card">
          <div class="avatar">IJ</div>
          <div class="name">Firstname<br>Lastname</div>
          <div class="role">Student</div>
          <a href="https://instagram.com/" target="_blank">@handle</a>
        </div>
        <div class="team-card">
          <div class="avatar">KL</div>
          <div class="name">Firstname<br>Lastname</div>
          <div class="role">Student</div>
          <a href="https://instagram.com/" target="_blank">@handle</a>
        </div>
      </div>

      <div class="divider-label">Professors</div>

      <div class="team-grid">
        <div class="team-card">
          <div class="avatar">PQ</div>
          <div class="name">Prof. Firstname<br>Lastname</div>
          <div class="role">Professor</div>
        </div>
        <div class="team-card">
          <div class="avatar">RS</div>
          <div class="name">Prof. Firstname<br>Lastname</div>
          <div class="role">Professor</div>
        </div>
        <div class="team-card">
          <div class="avatar">TU</div>
          <div class="name">Prof. Firstname<br>Lastname</div>
          <div class="role">Professor</div>
        </div>
      </div>
    </section>

  </main>

  <!-- ─── Footer ────────────────────────────────────────────── -->
  <footer>
    © 2025 &nbsp;·&nbsp; Inflatable Structure &nbsp;·&nbsp; [Your University / Department]
  </footer>

  <!-- ─── Lightbox ──────────────────────────────────────────── -->
  <div id="lightbox">
    <button id="lightbox-close">✕</button>
    <img id="lightbox-img" src="" alt="" />
  </div>

  <!-- ─── Scripts ──────────────────────────────────────────── -->
  <script>
    /* Intersection Observer — fade-in sections on scroll */
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(e => {
        if (e.isIntersecting) {
          e.target.classList.add('visible');
          observer.unobserve(e.target);
        }
      });
    }, { threshold: 0.1 });

    document.querySelectorAll('main section').forEach(s => observer.observe(s));

    /* Lightbox for gallery items */
    const lightbox    = document.getElementById('lightbox');
    const lightboxImg = document.getElementById('lightbox-img');

    document.querySelectorAll('.gallery-item img').forEach(img => {
      img.addEventListener('click', () => {
        lightboxImg.src = img.src;
        lightboxImg.alt = img.alt;
        lightbox.classList.add('open');
      });
    });

    document.getElementById('lightbox-close').addEventListener('click', () => {
      lightbox.classList.remove('open');
    });

    lightbox.addEventListener('click', (e) => {
      if (e.target === lightbox) lightbox.classList.remove('open');
    });

    document.addEventListener('keydown', (e) => {
      if (e.key === 'Escape') lightbox.classList.remove('open');
    });
  </script>

</body>
</html>
