<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Aesthetic Password Entry</title>
  <style>
    :root{
      --bg1:#0f172a;
      --glass: rgba(255,255,255,0.06);
      --accent1:#7c3aed;
      --accent2:#06b6d4;
      --success:#10b981;
      --danger:#ef4444;
      --card-radius:18px;
      --glass-border:rgba(255,255,255,0.08);
    }
    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0;
      font-family:Inter, ui-sans-serif, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
      background: radial-gradient(1200px 600px at 10% 10%, rgba(124,58,237,0.12), transparent),
                  radial-gradient(1000px 500px at 90% 90%, rgba(6,182,212,0.08), transparent),
                  linear-gradient(180deg,var(--bg1) 0%, #071024 100%);
      color:#e6eef8;
      display:flex;
      align-items:center;
      justify-content:center;
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
      padding:32px;
    }

    .card{
      width:100%;
      max-width:420px;
      background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
      border-radius:var(--card-radius);
      padding:28px;
      box-shadow: 0 10px 30px rgba(2,6,23,0.6), inset 0 1px 0 rgba(255,255,255,0.02);
      border:1px solid var(--glass-border);
      backdrop-filter: blur(8px) saturate(130%);
      transition:transform .28s cubic-bezier(.2,.9,.2,1);
    }
    .card:hover{transform:translateY(-6px)}

    h1{font-size:20px;margin:0 0 8px 0}
    p.sub{margin:0 0 20px 0;color:rgba(230,238,248,0.72);font-size:13px}

    .input-row{position:relative;margin-bottom:14px}
    label{display:block;font-size:12px;color:rgba(230,238,248,0.75);margin-bottom:8px}
    input[type="password"]{
      width:100%;
      padding:12px 44px 12px 12px;
      border-radius:10px;
      border:1px solid rgba(255,255,255,0.06);
      background:linear-gradient(180deg, rgba(255,255,255,0.01), rgba(255,255,255,0.00));
      color:inherit;
      font-size:15px;
      outline:none;
      transition:box-shadow .15s, border-color .15s;
    }
    input:focus{box-shadow:0 6px 18px rgba(124,58,237,0.08);border-color:rgba(124,58,237,0.6)}

    .toggle{
      position:absolute;right:10px;top:36px;transform:translateY(-50%);
      background:transparent;border:0;color:rgba(230,238,248,0.7);cursor:pointer;font-size:13px;padding:6px;border-radius:8px
    }
    .toggle:focus{outline:2px solid rgba(124,58,237,0.18)}

    .meta{display:flex;align-items:center;justify-content:space-between;margin-top:16px}

    .btn{
      display:inline-flex;gap:10px;align-items:center;padding:10px 16px;border-radius:12px;border:0;cursor:pointer;font-weight:600;font-size:14px;
      background:linear-gradient(90deg,var(--accent1),var(--accent2));color:white;box-shadow:0 8px 20px rgba(12,18,36,0.45);
      transition:transform .12s,opacity .12s
    }
    .btn:active{transform:translateY(1px)}

    .feedback{margin-top:12px;padding:10px;border-radius:10px;font-size:13px;display:none}
    .feedback.show{display:block}
    .feedback.success{background:linear-gradient(180deg, rgba(16,185,129,0.12), rgba(16,185,129,0.06));color:var(--success);border:1px solid rgba(16,185,129,0.12)}
    .feedback.error{background:linear-gradient(180deg, rgba(239,68,68,0.08), rgba(239,68,68,0.04));color:var(--danger);border:1px solid rgba(239,68,68,0.12)}

    .corner-deco{position:absolute;right:-40px;top:-40px;width:120px;height:120px;border-radius:20px;background:conic-gradient(from 180deg at 50% 50%, rgba(124,58,237,0.08), rgba(6,182,212,0.06));filter:blur(18px);pointer-events:none}
  </style>
</head>
<body>
  <div style="position:relative;">
    <div class="corner-deco" aria-hidden="true"></div>
    <form class="card" id="pwForm" autocomplete="off" novalidate>
      <h1>Enter password to continue</h1>
      <p class="sub">This page is protected. Please enter your password to unlock the content.</p>

      <div class="input-row">
        <label for="password">Password</label>
        <input id="password" name="password" type="password" placeholder="•••••••••" required minlength="6" />
      </div>

      <div class="meta">
        <button class="btn" type="submit">Enter</button>
      </div>

      <div id="feedback" class="feedback" role="status" aria-live="polite"></div>

    </form>
  </div>

  <script>
    const pw = document.getElementById('password');
    const feedback = document.getElementById('feedback');
    const form = document.getElementById('pwForm');

    const SECRET = 'I Love Myself';
    const REDIRECT_URL = 'https://example.com'; // Replace with your target page

    form.addEventListener('submit', (e)=>{
      e.preventDefault();
      const val = pw.value;
      if(val === SECRET){
    feedback.className = 'feedback success show';
    feedback.textContent = 'Password correct! Redirecting...';
    setTimeout(()=>{
      window.location.href = 'hbd.html';
    }, 1000);
} else {
    feedback.className = 'feedback error show';
    feedback.textContent = 'Incorrect password. Try again.';
}
    });
  </script>
</body>
</html>
