x; border-radius:8px; border:1px solid rgba(255,255,255,0.04); background:transparent; color:#fff;}
  .small-input{width:160px;}
  .customize{display:flex; gap:12px; align-items:center; margin-top:8px;}
  .color{display:flex; gap:6px; align-items:center;}
  label{font-size:13px; color:var(--muted);}
  footer{margin-top:16px; color:var(--muted); font-size:13px;}
  .kbd{background:#0a0a0b; padding:6px 8px; border-radius:6px; font-family:monospace; font-size:13px;}
  @media (max-width:640px){
    .flex{flex-direction:column; align-items:stretch;}
    .logo{width:56px;height:56px;font-size:18px;}
  }
</style>
</head>
<body>
  <div class="wrap">
    <header>
      <div class="logo">LIPS</div>
      <div>
        <h1>Booking — Lip Studio</h1>
        <p class="lead">Quick bookings and secure deposits. Send deposit, then submit the short form to lock your spot.</p>
      </div>
    </header>

    <!-- Payment area -->
    <div class="card">
      <h3 style="margin:0 0 8px 0;">Step 1 — Send your deposit</h3>
      <div class="buttons" style="margin-bottom:8px;">
        <!-- replace href with your cash app link -->
        <a class="btn btn-pay" id="cashLink" href="https://cash.app/$elgortito/50" target="_blank" rel="noopener noreferrer">
          Pay $50 — Cash App
        </a>
        <!-- Zelle: use mailto or plain text anchor; replace ZELLE_INFO -->
        <a class="btn btn-alt" id="zelleInfo" href="mailto:katiefiller@example.com?subject=Zelle%20Deposit" target="_blank" rel="noopener noreferrer">
          Zelle — katiefiller@example.com
        </a>
        <!-- Venmo could be another button; change as needed -->
        <a class="btn btn-alt" id="venmoBtn" href="#" onclick="alert('Venmo link not set');return false">Venmo</a>
      </div>
      <small>Send the $50 deposit, then complete the booking form below and upload screenshot of payment. Deposits are non-refundable and secure your spot.</small>
    </div>

    <!-- Booking Form embed (Google Form) -->
    <div class="card">
      <h3 style="margin:0 0 8px 0;">Step 2 — Complete booking form</h3>
      <p class="note">Fill this after you send deposit. The form collects Name, Service, Preferred Date(s), Payment Method, and accepts a payment screenshot upload.</p>

      <!-- Replace the src attribute with your Google Form Embed URL -->
      <iframe id="gform" src="FORM_EMBED_URL">Loading…</iframe>
      <small>If you need help making the Google Form and getting the embed URL, see the instructions at the bottom.</small>
    </div>

    <!-- Simple color customizer -->
    <div class="card">
      <div style="display:flex; align-items:center; justify-content:space-between; gap:12px; flex-wrap:wrap;">
        <div>
          <h3 style="margin:0 0 6px 0;">Brand color customizer</h3>
          <p class="note">Pick colors — copy the CSS variables below and paste into the site's stylesheet or your host custom CSS.</p>
        </div>
        <div class="customize">
          <div class="color">
            <label for="c1">Accent 1</label>
            <input type="color" id="c1" value="#e75480">
          </div>
          <div class="color">
            <label for="c2">Accent 2</label>
            <input type="color" id="c2" value="#2d6cdf">
          </div>
          <div class="color">
            <label for="bg">BG</label>
            <input type="color" id="bg" value="#0f0f12">
          </div>
        </div>
      </div>
      <div style="margin-top:12px;">
        <div class="kbd" id="cssOut">/* CSS will appear here after you pick colors */</div>
      </div>
    </div>

    <footer>
      <div>Site shows a generic brand name so the studio owner’s personal name is not visible. Replace any text in the header with your chosen brand label.</div>
      <div style="margin-top:8px;">
        <strong>Make & embed Google Form</strong><br/>
        1. Create form at <span class="kbd">forms.google.com</span>. Fields: Full Name, Phone, IG handle, Service (dropdown), Preferred Date(s), Payment Method (dropdown), Upload (file).<br/>
        2. Click Send → &lt;&gt; (embed) → Copy the iframe src (the URL inside src="...") and replace the <span class="kbd">FORM_EMBED_URL</span> placeholder above.<br/>
        3. Put the site's URL in your IG/TikTok bio. Pin this site link in your comments and posts.
      </div>
    </footer>
  </div>

<script>
  // Color customizer JS: updates CSS vars live and prints CSS snippet
  const c1 = document.getElementById('c1');
  const c2 = document.getElementById('c2');
  const bg = document.getElementById('bg');
  const cssOut = document.getElementById('cssOut');

  function updateColors(){
    document.documentElement.style.setProperty('--accent', c1.value);
    document.documentElement.style.setProperty('--accent-2', c2.value);
    document.documentElement.style.setProperty('--bg', bg.value);
    const snippet = `
:root{
  --bg: ${bg.value};
  --card: ${shadeColor(bg.value, 8)};
  --muted: #cfcfcf;
  --accent: ${c1.value};
  --accent-2: ${c2.value};
}
    `.trim();
    cssOut.textContent = snippet;
  }

  // helper to darken the card background slightly
  function shadeColor(hex, percent) {
    // hex format #rrggbb
    const num = parseInt(hex.replace('#',''),16);
    const r = Math.max(0, (num >> 16) - percent);
    const g = Math.max(0, ((num >> 8) & 0x00FF) - percent);
    const b = Math.max(0, (num & 0x0000FF) - percent);
    return '#' + ( (1<<24) + (r<<16) + (g<<8) + b ).toString(16).slice(1);
  }

  [c1,c2,bg].forEach(i => i.addEventListener('input', updateColors));
  updateColors();

  // small helper to let you change the payment links quickly (optionally)
  function setPayments({cash, zelle, venmo}){
    if(cash) document.getElementById('cashLink').href = cash;
    if(zelle) document.getElementById('zelleInfo').href = zelle;
    if(venmo) document.getElementById('venmoBtn').href = venmo;
  }

  // Uncomment and set real links if you'd rather set them inside the file:
  // setPayments({cash:'https://cash.app/$elgortito/50', zelle:'mailto:katiefiller@example.com?subject=Zelle%20Deposit', venmo:'https://venmo.com/YourUser?txn=pay'});

</script>
</body>
</html>
