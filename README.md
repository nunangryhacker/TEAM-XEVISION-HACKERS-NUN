<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Nun Angry Hackers TXH — README</title>
  <style>
    :root{
      --bg:#000;
      --neon:#33ff66;
      --muted:#7af0a6;
      --panel:#071009;
      --accent:#8fffbe;
      --mono: "Source Code Pro", Consolas, Monaco, "Courier New", monospace;
    }
    html,body{height:100%;margin:0;background:var(--bg);color:var(--neon);font-family:var(--mono);}
    .wrap{display:flex;flex-direction:column;min-height:100vh;gap:18px;padding:24px;}
    header{display:flex;align-items:center;gap:18px}
    .logo{
      width:88px;height:88px;border-radius:8px;
      background:linear-gradient(135deg,#04210a 0%, rgba(3,10,6,0.4) 60%);
      box-shadow:0 0 18px rgba(51,255,102,0.08), inset 0 0 40px rgba(51,255,102,0.03);
      display:flex;align-items:center;justify-content:center;font-weight:700;
      color:var(--panel);font-size:16px;
    }
    h1{margin:0;font-size:20px;letter-spacing:1px}
    p.lead{margin:0;color:var(--muted)}
    .panel{background:linear-gradient(180deg, rgba(7,16,9,0.6), rgba(5,10,7,0.4));border-radius:10px;padding:16px;box-shadow:0 6px 30px rgba(0,0,0,0.6);border:1px solid rgba(51,255,102,0.06)}
    .columns{display:grid;grid-template-columns:1fr 380px;gap:16px;align-items:start}
    .section-title{color:var(--accent);font-weight:700;margin-bottom:8px}
    pre.code{background:rgba(0,0,0,0.6);padding:12px;border-radius:8px;overflow:auto;border:1px solid rgba(51,255,102,0.06);font-size:13px}
    .team-list{list-style:none;padding:0;margin:0;display:grid;gap:8px}
    .team-list li{padding:6px;border-radius:6px;background:rgba(255,255,255,0.02);border:1px dashed rgba(51,255,102,0.03)}
    .muted{color:rgba(51,255,102,0.45);font-size:13px}
    .btn{display:inline-block;padding:8px 12px;border-radius:8px;background:transparent;border:1px solid rgba(51,255,102,0.12);color:var(--neon);cursor:pointer;font-family:var(--mono);font-size:13px}
    .btn:hover{box-shadow:0 0 18px rgba(51,255,102,0.06)}
    footer{margin-top:auto;color:rgba(51,255,102,0.18);font-size:13px;padding:12px 0}
    .matrix-canvas{width:100%;height:220px;border-radius:8px;display:block}
    .artifact{display:flex;gap:8px;flex-direction:column}
    .artifact .controls{display:flex;gap:8px;align-items:center}
    .timestamp{color:var(--muted);font-size:12px}
    details summary{cursor:pointer;outline:none;padding:8px;background:rgba(255,255,255,0.01);border-radius:6px;border:1px solid rgba(51,255,102,0.03)}
    .copy-btn{padding:6px;border-radius:6px;background:transparent;border:1px solid rgba(51,255,102,0.06);cursor:pointer}
    /* responsive */
    @media (max-width:900px){ .columns{grid-template-columns:1fr} .matrix-canvas{height:160px} .logo{width:64px;height:64px;font-size:13px} }
  </style>
</head>
<body>
  <div class="wrap">
    <header>
      <div class="logo">TXH</div>
      <div>
        <h1>Nun Angry Hackers TXH — <span style="color:var(--accent)">SYSTEM: REBOOT</span></h1>
        <p class="lead">code cold, intent hot. ethic by choice, chaos by craft.</p>
      </div>
    </header>

    <div class="columns">
      <main class="panel">
        <canvas id="matrix" class="matrix-canvas"></canvas>

        <section style="margin-top:14px">
          <div class="section-title">About</div>
          <p class="muted">A midnight collective that finds brittle code, documents failure modes, and ships fixes. We play CTFs, practice responsible disclosure, and craft defensive tooling.</p>
        </section>

        <section style="margin-top:12px">
          <div class="section-title">Mission</div>
          <ul class="muted" style="margin:6px 0 0 18px">
            <li>Expose fragility so it can be fixed.</li>
            <li>Publish PoCs & writeups for education — never for unlawful use.</li>
            <li>Responsible disclosure first; public after patch or coordinated disclosure.</li>
            <li>Win CTFs. Teach others. Break things in the lab, not in the wild.</li>
          </ul>
        </section>

        <section style="margin-top:12px">
          <div class="section-title">Team (aliases)</div>
          <ul class="team-list">
            <li><strong>Sister0x</strong> — recon & opsec</li>
            <li><strong>AngryNun</strong> — reverse engineering & firmware spelunking</li>
            <li><strong>TXH_Shadow</strong> — exploit prototyping (research-only)</li>
            <li><strong>PatchPriest</strong> — blue-team, mitigations, playbooks</li>
            <li><strong>glitch.py</strong> — automation & CI trickster</li>
          </ul>
        </section>

        <section style="margin-top:12px">
          <div class="section-title">Rules of Engagement</div>
          <ol class="muted" style="margin-left:18px">
            <li>No illegal ops — research in labs, CTFs, or with explicit permission.</li>
            <li>Responsible disclosure — coordinate with vendors before public release for real vulnerabilities.</li>
            <li>No black-hat services — we do not sell exploitation for hire.</li>
          </ol>
        </section>

        <section style="margin-top:12px">
          <div style="display:flex;justify-content:space-between;align-items:center">
            <div class="section-title">System: Reboot (THEATRICAL, SAFE)</div>
            <div class="timestamp" id="local-time"></div>
          </div>

          <div class="artifact" style="margin-top:8px">
            <div class="controls">
              <button class="btn" id="start-reboot">Run SYSTEM: REBOOT (simulate)</button>
              <button class="btn" id="stop-reboot" disabled>Stop</button>
              <button class="btn" id="clear-output">Clear</button>
              <span style="flex:1"></span>
              <button class="btn" id="copy-output">Copy Output</button>
            </div>

            <pre id="reboot-output" class="code" style="height:190px;white-space:pre-wrap;overflow:auto">
<!-- Output stream: simulation only. --> 
            </pre>

            <details style="margin-top:8px">
              <summary>View theatrical demo files (read-only)</summary>

              <div style="margin-top:8px">
                <div class="section-title" style="font-size:13px">system_reboot.sh (demo)</div>
                <pre class="code" id="file-system-reboot" style="height:200px;white-space:pre-wrap;overflow:auto">
#!/usr/bin/env bash
# system_reboot.sh — NUN ANGRY HACKERS TXH (simulation)
# Purpose: theatrical matrix reboot sequence — NON-DESTRUCTIVE

set -euo pipefail

banner() {
  cat <<'BANNER'

========================================
   NUN ANGRY HACKERS TXH — SYSTEM: REBOOT
========================================

BANNER
}

matrix_echo() {
  for i in $(seq 1 30); do
    head -c 16 /dev/urandom | xxd -p | tr -d '\n'
    printf "  |  %s\n" "$(date '+%H:%M:%S')"
    sleep 0.04
  done
}

soft_reboot() {
  echo "[..] Saving state (simulated)"
  sleep 0.3
  echo "[..] Flushing caches (simulated)"
  sleep 0.3
  echo "[..] Restarting daemons (simulated)"
  sleep 0.4
}

banner
matrix_echo
soft_reboot

echo
echo "[ OK ] SYSTEM: REBOOT — simulation complete"
echo "TXH — keep it ethical. Responsible disclosure or GTFO."
                </pre>
              </div>

              <div style="margin-top:10px">
                <div class="section-title" style="font-size:13px">time_relay.txt (decorative)</div>
                <pre class="code" id="file-time-relay" style="height:120px;white-space:pre-wrap;overflow:auto">
--- TIME RE-LAY v1 ---
UTC: <!-- dynamic -->
Epoch: <!-- dynamic -->
Sync: TXH-NTP // last_synced: simulated
Message: "When clocks unwind, we patch the hole."
----------------------
                </pre>
              </div>
            </details>
          </div>
        </section>

        <section style="margin-top:12px;display:flex;justify-content:space-between;align-items:center">
          <div>
            <div class="muted">Tech Stack: Python · Rust · Go · Bash · C/C++</div>
            <div class="muted">Toys: Ghidra · radare2 · IDA · Burp · Wireshark · custom fuzzers</div>
          </div>
          <div style="text-align:right">
            <div style="font-size:12px;color:var(--muted)">© 2025 Nun Angry Hackers TXH</div>
            <div style="font-size:11px;color:rgba(51,255,102,0.14)">All rights reserved. Use requires permission.</div>
          </div>
        </section>
      </main>

      <aside class="panel">
        <div class="section-title">Quick Links</div>
        <div style="display:flex;flex-direction:column;gap:8px;margin-top:8px">
          <button class="btn" id="download-html">Download HTML</button>
          <button class="btn" id="download-reboot">Download system_reboot.sh</button>
          <button class="btn" id="download-time">Download time_relay.txt</button>
          <button class="btn" id="toggle-matrix">Toggle Matrix</button>
        </div>

        <div style="margin-top:14px">
          <div class="section-title">Contact</div>
          <div class="muted">PRs & issues welcome. For sensitive security reports, use a vetted secure channel (PGP/GPG recommended).</div>
          <div style="margin-top:8px;font-size:13px">security[at]nunangryhackers[dot]txh</div>
        </div>

        <details style="margin-top:12px">
          <summary>TL;DR</summary>
          <p class="muted" style="margin-top:8px">We find the gaps, document the fall, and ship the fix. Rogue aesthetic. Ethical practice. No drama — just craft.</p>
        </details>
      </aside>
    </div>

    <footer>
      <div>Built for vibe & safety — all simulations are non-destructive. © 2025 Nun Angry Hackers TXH — All rights reserved.</div>
    </footer>
  </div>

  <script>
    // Matrix effect
    (function(){
      const canvas = document.getElementById('matrix');
      const ctx = canvas.getContext('2d');
      let w, h, cols, ypos, animationId;
      function resize(){
        w = canvas.width = canvas.clientWidth * devicePixelRatio;
        h = canvas.height = canvas.clientHeight * devicePixelRatio;
        ctx.scale(devicePixelRatio, devicePixelRatio);
        cols = Math.floor(canvas.clientWidth / 14);
        ypos = new Array(cols).fill(0);
      }
      function draw(){
        ctx.fillStyle = 'rgba(0,0,0,0.06)';
        ctx.fillRect(0,0,canvas.clientWidth,canvas.clientHeight);
        ctx.fillStyle = 'rgba(51,255,102,0.9)';
        ctx.font = '13px monospace';
        for(let i=0;i<ypos.length;i++){
          const text = Math.random() > 0.5 ? (Math.random().toString(16).slice(2,10)) : String.fromCharCode(48 + Math.floor(Math.random()*10));
          const x = i * 14;
          const y = ypos[i] * 14;
          ctx.fillText(text.slice(0,8), x, y);
          if(y > canvas.clientHeight + Math.random()*1000) ypos[i]=0;
          ypos[i]++;
        }
        animationId = requestAnimationFrame(draw);
      }
      window.addEventListener('resize', () => { cancelAnimationFrame(animationId); resize(); draw(); });
      resize(); draw();

      // Toggle
      window.toggleMatrix = function(){
        if(animationId){ cancelAnimationFrame(animationId); animationId = null; ctx.clearRect(0,0,canvas.width,canvas.height); }
        else draw();
      };
    })();

    // Reboot simulation: harmless
    (function(){
      const out = document.getElementById('reboot-output');
      const start = document.getElementById('start-reboot');
      const stop = document.getElementById('stop-reboot');
      const clearBtn = document.getElementById('clear-output');
      const copyBtn = document.getElementById('copy-output');
      const timeEl = document.getElementById('local-time');
      let interval=null;
      function now(){ return new Date().toLocaleString(); }
      function hexLine(){
        // simple pseudo-hex generator
        const arr = new Uint8Array(8);
        crypto.getRandomValues(arr);
        return Array.from(arr).map(b=>b.toString(16).padStart(2,'0')).join('');
      }
      function appendLine(s){
        out.textContent += s + "\\n";
        out.scrollTop = out.scrollHeight;
      }
      start.addEventListener('click', ()=>{
        start.disabled = true; stop.disabled = false;
        appendLine("========================================");
        appendLine("  NUN ANGRY HACKERS TXH — SYSTEM: REBOOT");
        appendLine("========================================");
        let counter=0;
        interval = setInterval(()=>{
          appendLine(hexLine() + "  |  " + new Date().toLocaleTimeString());
          counter++;
          if(counter===10){
            appendLine("[..] Saving state... (simulated)");
          } else if(counter===18){
            appendLine("[..] Flushing caches... (simulated)");
          } else if(counter===26){
            appendLine("[..] Restarting services... (simulated)");
          } else if(counter>32){
            appendLine("");
            appendLine("[ OK ] SYSTEM: REBOOT (simulation complete)");
            appendLine("TXH — keep it ethical. Responsible disclosure or GTFO.");
            clearInterval(interval); interval=null;
            start.disabled = false; stop.disabled = true;
          }
        }, 120);
      });
      stop.addEventListener('click', ()=>{
        if(interval) clearInterval(interval);
        interval=null;
        appendLine("[ .. ] SIMULATION: aborted by operator.");
        start.disabled=false; stop.disabled=true;
      });
      clearBtn.addEventListener('click', ()=>{ out.textContent = ""; });
      copyBtn.addEventListener('click', async ()=>{
        try{
          await navigator.clipboard.writeText(out.textContent);
          copyBtn.textContent = 'Copied ✓';
          setTimeout(()=> copyBtn.textContent='Copy Output',900);
        }catch(e){
          copyBtn.textContent = 'Copy failed';
          setTimeout(()=> copyBtn.textContent='Copy Output',900);
        }
      });

      // Fill time_relay content dynamically
      const tfile = document.getElementById('file-time-relay');
      const epoch = Math.floor(Date.now()/1000);
      tfile.textContent = [
        '--- TIME RE-LAY v1 ---',
        'UTC: ' + new Date().toISOString(),
        'Epoch: ' + epoch,
        'Sync: TXH-NTP // last_synced: simulated',
        'Message: "When clocks unwind, we patch the hole."',
        '----------------------'
      ].join('\\n');

      // local time display
      const localTime = document.getElementById('local-time');
      function tick(){ localTime.textContent = new Date().toLocaleString(); }
      tick(); setInterval(tick,1000);

      // Download helpers
      document.getElementById('download-html').addEventListener('click', ()=>{
        const blob = new Blob([document.documentElement.outerHTML], {type:'text/html'});
        const url = URL.createObjectURL(blob);
        const a = document.createElement('a'); a.href=url; a.download = 'README.html'; a.click();
        URL.revokeObjectURL(url);
      });
      document.getElementById('download-reboot').addEventListener('click', ()=>{
        const content = document.getElementById('file-system-reboot').textContent.trim();
        const blob = new Blob([content], {type:'text/x-sh'});
        const url = URL.createObjectURL(blob);
        const a = document.createElement('a'); a.href=url; a.download = 'system_reboot.sh'; a.click();
        URL.revokeObjectURL(url);
      });
      document.getElementById('download-time').addEventListener('click', ()=>{
        const content = document.getElementById('file-time-relay').textContent.trim();
        const blob = new Blob([content], {type:'text/plain'});
        const url = URL.createObjectURL(blob);
        const a = document.createElement('a'); a.href=url; a.download = 'time_relay.txt'; a.click();
        URL.revokeObjectURL(url);
      });
      document.getElementById('toggle-matrix').addEventListener('click', ()=>{ window.toggleMatrix(); });

      // Copy code blocks quick-copy
      document.getElementById('copy-output').addEventListener('click', ()=>{}); // handled above
    })();
  </script>
</body>
</html>
