<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Coffee Order Activity</title>
  <style>
    :root{--bg:#0b0c10;--card:#14161d;--muted:#9aa3b2;--text:#eef2ff;--accent:#7c3aed;--good:#22c55e;--warn:#f59e0b;--bad:#ef4444;--line:#262a36}
    *{box-sizing:border-box}
    body{margin:0;font-family:system-ui,-apple-system,Segoe UI,Roboto,Arial,sans-serif;background:linear-gradient(180deg,#0b0c10,#0b0c10 30%,#0f1220);color:var(--text)}
    .wrap{max-width:980px;margin:0 auto;padding:16px}
    header{display:flex;gap:12px;align-items:center;justify-content:space-between;flex-wrap:wrap;margin:8px 0 16px}
    .brand{display:flex;align-items:center;gap:10px}
    .logo{width:38px;height:38px;border-radius:12px;background:radial-gradient(circle at 30% 30%,#a78bfa,#7c3aed 60%,#4c1d95);box-shadow:0 10px 24px rgba(124,58,237,.35)}
    h1{font-size:18px;margin:0}
    .sub{color:var(--muted);font-size:13px;margin-top:2px}
    .pill{border:1px solid var(--line);background:rgba(255,255,255,.03);padding:8px 10px;border-radius:999px;display:flex;gap:8px;align-items:center}
    .pill label{font-size:13px;color:var(--muted)}
    .pill input{transform:scale(1.1)}

    .grid{display:grid;grid-template-columns:1.2fr .8fr;gap:14px}
    @media (max-width:860px){.grid{grid-template-columns:1fr}}

    .card{background:rgba(255,255,255,.04);border:1px solid var(--line);border-radius:18px;padding:14px;box-shadow:0 12px 30px rgba(0,0,0,.25)}
    .card h2{font-size:15px;margin:0 0 10px}
    .muted{color:var(--muted);font-size:13px}

    .menu{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:10px}
    @media (max-width:430px){.menu{grid-template-columns:1fr}}
    .item{border:1px solid var(--line);background:rgba(0,0,0,.25);border-radius:14px;padding:10px;cursor:pointer;transition:transform .05s ease,border-color .2s ease}
    .item:hover{border-color:rgba(124,58,237,.8)}
    .item:active{transform:scale(.99)}
    .item strong{display:block;font-size:14px}
    .item small{color:var(--muted)}

    .row{display:grid;grid-template-columns:1fr 1fr;gap:10px}
    @media (max-width:520px){.row{grid-template-columns:1fr}}

    select,input[type="text"],input[type="number"]{width:100%;padding:10px 12px;border-radius:12px;border:1px solid var(--line);background:rgba(0,0,0,.25);color:var(--text);outline:none}
    select:focus,input:focus{border-color:rgba(124,58,237,.9)}

    .btns{display:flex;gap:10px;flex-wrap:wrap}
    button{border:0;border-radius:12px;padding:10px 12px;font-weight:650;color:var(--text);background:rgba(255,255,255,.07);cursor:pointer;border:1px solid var(--line)}
    button.primary{background:linear-gradient(135deg,#7c3aed,#5b21b6);border-color:rgba(124,58,237,.9)}
    button.good{background:rgba(34,197,94,.18);border-color:rgba(34,197,94,.45)}
    button.warn{background:rgba(245,158,11,.16);border-color:rgba(245,158,11,.45)}
    button.bad{background:rgba(239,68,68,.14);border-color:rgba(239,68,68,.45)}
    button:disabled{opacity:.55;cursor:not-allowed}

    .statusLine{display:flex;gap:8px;align-items:center;flex-wrap:wrap}
    .dot{width:9px;height:9px;border-radius:50%;background:var(--muted)}
    .dot.on{background:var(--accent);box-shadow:0 0 0 4px rgba(124,58,237,.18)}
    .step{font-size:13px;color:var(--muted)}
    .step.on{color:var(--text);font-weight:650}

    .price{display:flex;justify-content:space-between;align-items:center;border-top:1px solid var(--line);margin-top:12px;padding-top:10px}
    .price strong{font-size:16px}

    .hist{display:flex;flex-direction:column;gap:10px}
    .histItem{border:1px solid var(--line);background:rgba(0,0,0,.2);border-radius:14px;padding:10px}
    .histItem .top{display:flex;justify-content:space-between;gap:10px}
    .tag{font-size:12px;color:var(--muted)}

    .toast{position:fixed;left:50%;bottom:16px;transform:translateX(-50%);background:rgba(20,22,29,.95);border:1px solid var(--line);padding:10px 12px;border-radius:14px;max-width:92vw;display:none}
    .toast.show{display:block}
  </style>
</head>
<body>
  <div class="wrap">
    <header>
      <div class="brand">
        <div class="logo" aria-hidden="true"></div>
        <div>
          <h1>Coffee Order Activity</h1>
          <div class="sub">A simple “app” to practice the full ordering flow (menu → customise → pay → status → pickup → history).</div>
        </div>
      </div>

      <div class="pill" title="Turn this on to demonstrate the barista side">
        <label for="baristaToggle">Barista mode</label>
        <input id="baristaToggle" type="checkbox" />
      </div>
    </header>

    <div class="grid">
      <section class="card">
        <h2>1) Choose a drink</h2>
        <div class="menu" id="menu"></div>

        <div style="height:12px"></div>

        <h2>2) Customise</h2>
        <div class="row">
          <div>
            <div class="muted">Milk type</div>
            <select id="milk">
              <option>Whole</option>
              <option>Semi-skimmed</option>
              <option>Skimmed</option>
              <option>Oat</option>
              <option>Almond</option>
              <option>Soya</option>
            </select>
          </div>
          <div>
            <div class="muted">Size</div>
            <select id="size">
              <option value="S">Small</option>
              <option value="M" selected>Medium</option>
              <option value="L">Large</option>
            </select>
          </div>
        </div>

        <div style="height:10px"></div>

        <div class="row">
          <div>
            <div class="muted">Syrup</div>
            <select id="syrup">
              <option value="None">None</option>
              <option value="Vanilla">Vanilla</option>
              <option value="Caramel">Caramel</option>
              <option value="Hazelnut">Hazelnut</option>
            </select>
          </div>
          <div>
            <div class="muted">Extra shots</div>
            <select id="shots">
              <option value="0">0</option>
              <option value="1">1</option>
              <option value="2">2</option>
            </select>
          </div>
        </div>

        <div style="height:10px"></div>
        <div class="muted">Note (optional)</div>
        <input id="note" type="text" placeholder="e.g., less foam / extra hot" maxlength="60" />

        <div class="price">
          <div>
            <div class="muted">Estimated total</div>
            <strong id="total">£0.00</strong>
          </div>
          <div class="btns">
            <button id="clearBtn">Reset</button>
            <button class="primary" id="payBtn" disabled>3) Pay & place order</button>
          </div>
        </div>

        <div style="height:12px"></div>

        <h2>4) Live status</h2>
        <div class="statusLine" aria-live="polite">
          <span class="dot" id="d0"></span><span class="step" id="s0">Order received</span>
          <span class="muted">→</span>
          <span class="dot" id="d1"></span><span class="step" id="s1">Being made</span>
          <span class="muted">→</span>
          <span class="dot" id="d2"></span><span class="step" id="s2">Ready for pickup</span>
          <span class="muted">→</span>
          <span class="dot" id="d3"></span><span class="step" id="s3">Completed</span>
        </div>

        <div style="height:10px"></div>
        <div class="btns" id="baristaControls" style="display:none">
          <button class="warn" id="nextStatusBtn" disabled>Barista: Next status</button>
          <button class="good" id="completeBtn" disabled>Mark completed</button>
          <button class="bad" id="cancelBtn" disabled>Cancel order</button>
        </div>

        <div style="height:6px"></div>
        <div class="muted" id="statusMsg">No active order yet. Choose a drink and pay to start.</div>
      </section>

      <aside class="card">
        <h2>Order history & rewards</h2>
        <div class="muted">Orders are stored on this phone only (using <b>localStorage</b>) so students can see how apps remember history.</div>

        <div style="height:10px"></div>
        <div class="card" style="padding:12px;border-radius:16px">
          <div class="muted">Reward points</div>
          <div style="display:flex;justify-content:space-between;align-items:end;gap:10px">
            <div>
              <div style="font-size:26px;font-weight:800" id="points">0</div>
              <div class="muted" style="margin-top:-2px">10 points per completed order</div>
            </div>
            <button id="clearHistoryBtn">Clear history</button>
          </div>
        </div>

        <div style="height:10px"></div>
        <div class="hist" id="history"></div>

        <div style="height:10px"></div>
        <div class="card" style="padding:12px;border-radius:16px">
          <div style="font-weight:700">Teacher prompt (quick)</div>
          <div class="muted" style="margin-top:6px">
            Ask students to identify: <b>Inputs</b> (choices), <b>Processing</b> (pricing + status), <b>Outputs</b> (receipt + updates), and <b>Storage</b> (order history for rewards/recommendations).
          </div>
        </div>
      </aside>
    </div>
  </div>

  <div class="toast" id="toast"></div>

  <script>
    // --- Simple “coffee ordering” simulation (single-file, no backend) ---

    const MENU = [
      { name: "Latte", base: 3.20, desc: "Smooth espresso + milk" },
      { name: "Cappuccino", base: 3.10, desc: "Foamy classic" },
      { name: "Americano", base: 2.80, desc: "Espresso + hot water" },
      { name: "Mocha", base: 3.40, desc: "Chocolate + espresso" },
      { name: "Flat White", base: 3.30, desc: "Strong and silky" },
      { name: "Hot Chocolate", base: 3.00, desc: "No кофе? still cosy" },
    ];

    const $ = (id) => document.getElementById(id);

    // UI refs
    const menuEl = $("menu");
    const milkEl = $("milk");
    const sizeEl = $("size");
    const syrupEl = $("syrup");
    const shotsEl = $("shots");
    const noteEl = $("note");
    const totalEl = $("total");
    const payBtn = $("payBtn");
    const clearBtn = $("clearBtn");

    const baristaToggle = $("baristaToggle");
    const baristaControls = $("baristaControls");
    const nextStatusBtn = $("nextStatusBtn");
    const completeBtn = $("completeBtn");
    const cancelBtn = $("cancelBtn");

    const statusMsg = $("statusMsg");
    const historyEl = $("history");
    const pointsEl = $("points");
    const clearHistoryBtn = $("clearHistoryBtn");

    // state
    let selected = null;
    let activeOrder = null; // { id, drink, options, total, statusIndex, createdAt }
    let timers = [];

    const STATUS = ["Order received", "Being made", "Ready for pickup", "Completed"];

    function money(n){
      return new Intl.NumberFormat("en-GB", { style: "currency", currency: "GBP" }).format(n);
    }

    function toast(msg){
      const t = $("toast");
      t.textContent = msg;
      t.classList.add("show");
      setTimeout(() => t.classList.remove("show"), 2200);
    }

    function priceForSelection(){
      if(!selected) return 0;
      const size = sizeEl.value;
      const syrup = syrupEl.value;
      const shots = parseInt(shotsEl.value, 10);

      const sizeExtra = size === "S" ? 0 : size === "M" ? 0.30 : 0.60;
      const syrupExtra = syrup === "None" ? 0 : 0.35;
      const shotsExtra = shots * 0.55;

      return +(selected.base + sizeExtra + syrupExtra + shotsExtra).toFixed(2);
    }

    function renderMenu(){
      menuEl.innerHTML = "";
      MENU.forEach((m) => {
        const div = document.createElement("button");
        div.className = "item";
        div.type = "button";
        div.innerHTML = `<strong>${m.name}</strong><small>${m.desc} • from ${money(m.base)}</small>`;
        div.addEventListener("click", () => {
          selected = m;
          [...menuEl.querySelectorAll(".item")].forEach(x => x.style.borderColor = "var(--line)");
          div.style.borderColor = "rgba(124,58,237,.9)";
          updateTotal();
          toast(`${m.name} selected`);
        });
        menuEl.appendChild(div);
      });
    }

    function updateTotal(){
      const total = priceForSelection();
      totalEl.textContent = money(total);
      payBtn.disabled = !selected || !!activeOrder;
    }

    function clearTimers(){
      timers.forEach(t => clearTimeout(t));
      timers = [];
    }

    function setStatus(index){
      if(!activeOrder) return;
      activeOrder.statusIndex = index;
      syncActiveOrder();
      renderStatus();
    }

    function renderStatus(){
      const idx = activeOrder ? activeOrder.statusIndex : -1;
      for(let i=0;i<4;i++){
        const dot = $("d"+i);
        const step = $("s"+i);
        const on = idx >= i && idx !== -1;
        dot.className = "dot" + (on ? " on" : "");
        step.className = "step" + (on ? " on" : "");
      }

      const hasActive = !!activeOrder;
      nextStatusBtn.disabled = !hasActive || activeOrder.statusIndex >= 2; // stop at Ready
      completeBtn.disabled = !hasActive || activeOrder.statusIndex < 2;
      cancelBtn.disabled = !hasActive;

      if(!activeOrder){
        statusMsg.textContent = "No active order yet. Choose a drink and pay to start.";
      } else {
        statusMsg.textContent = `Order #${activeOrder.id} • ${activeOrder.drink} • ${STATUS[activeOrder.statusIndex]}`;
      }
    }

    function newOrder(){
      const total = priceForSelection();
      const options = {
        milk: milkEl.value,
        size: sizeEl.options[sizeEl.selectedIndex].text,
        syrup: syrupEl.value,
        shots: parseInt(shotsEl.value,10),
        note: noteEl.value.trim(),
      };

      activeOrder = {
        id: String(Math.floor(Math.random()*9000)+1000),
        drink: selected.name,
        options,
        total,
        statusIndex: 0,
        createdAt: new Date().toISOString(),
      };

      syncActiveOrder();
      renderStatus();
      payBtn.disabled = true;

      // Simulate the coffee shop receiving and making the drink.
      // (In class: discuss that a real system would send this to a server and barista screen.)
      clearTimers();
      timers.push(setTimeout(() => setStatus(1), 4500));
      timers.push(setTimeout(() => setStatus(2), 9500));

      toast("Payment successful (simulated) — order sent to coffee shop");
    }

    function completeOrder(){
      if(!activeOrder) return;
      setStatus(3);

      const hist = loadHistory();
      hist.unshift({ ...activeOrder, completedAt: new Date().toISOString() });
      saveHistory(hist);

      // Rewards: 10 points per completed order
      const pts = loadPoints() + 10;
      savePoints(pts);

      activeOrder = null;
      localStorage.removeItem("coffee_active_order");
      clearTimers();

      renderHistory();
      renderStatus();
      updateTotal();

      toast("Order completed — +10 points");
    }

    function cancelOrder(){
      if(!activeOrder) return;
      toast("Order cancelled");
      activeOrder = null;
      localStorage.removeItem("coffee_active_order");
      clearTimers();
      renderStatus();
      updateTotal();
    }

    // --- localStorage (History & points) ---
    function loadHistory(){
      try{ return JSON.parse(localStorage.getItem("coffee_history")||"[]") }catch{ return [] }
    }
    function saveHistory(hist){
      localStorage.setItem("coffee_history", JSON.stringify(hist.slice(0,12)));
    }
    function loadPoints(){
      return parseInt(localStorage.getItem("coffee_points")||"0",10);
    }
    function savePoints(n){
      localStorage.setItem("coffee_points", String(n));
      pointsEl.textContent = String(n);
    }
    function syncActiveOrder(){
      if(activeOrder) localStorage.setItem("coffee_active_order", JSON.stringify(activeOrder));
    }
    function loadActiveOrder(){
      try{ return JSON.parse(localStorage.getItem("coffee_active_order")||"null") }catch{ return null }
    }

    function renderHistory(){
      const hist = loadHistory();
      historyEl.innerHTML = "";
      if(hist.length === 0){
        const empty = document.createElement("div");
        empty.className = "muted";
        empty.textContent = "No completed orders yet.";
        historyEl.appendChild(empty);
      } else {
        hist.forEach((h) => {
          const div = document.createElement("div");
          div.className = "histItem";
          const when = new Date(h.completedAt||h.createdAt);
          const opts = `${h.options.size}, ${h.options.milk}, syrup: ${h.options.syrup}, shots: ${h.options.shots}${h.options.note?`, note: ${h.options.note}`:""}`;
          div.innerHTML = `
            <div class="top">
              <div><b>${h.drink}</b> <span class="tag">#${h.id}</span></div>
              <div><b>${money(h.total)}</b></div>
            </div>
            <div class="muted" style="margin-top:4px">${opts}</div>
            <div class="tag" style="margin-top:6px">Completed: ${when.toLocaleString()}</div>
          `;
          historyEl.appendChild(div);
        });
      }

      pointsEl.textContent = String(loadPoints());
    }

    // --- events ---
    [milkEl,sizeEl,syrupEl,shotsEl].forEach(el => el.addEventListener("change", updateTotal));
    clearBtn.addEventListener("click", () => {
      selected = null;
      [...menuEl.querySelectorAll(".item")].forEach(x => x.style.borderColor = "var(--line)");
      noteEl.value = "";
      milkEl.selectedIndex = 0;
      sizeEl.value = "M";
      syrupEl.value = "None";
      shotsEl.value = "0";
      updateTotal();
      toast("Reset");
    });

    payBtn.addEventListener("click", () => {
      if(!selected) return;
      newOrder();
    });

    baristaToggle.addEventListener("change", () => {
      const on = baristaToggle.checked;
      baristaControls.style.display = on ? "flex" : "none";
      toast(on ? "Barista mode on" : "Barista mode off");
    });

    nextStatusBtn.addEventListener("click", () => {
      if(!activeOrder) return;
      const next = Math.min(activeOrder.statusIndex + 1, 2);
      setStatus(next);
    });
    completeBtn.addEventListener("click", completeOrder);
    cancelBtn.addEventListener("click", cancelOrder);

    clearHistoryBtn.addEventListener("click", () => {
      localStorage.removeItem("coffee_history");
      savePoints(0);
      renderHistory();
      toast("History cleared");
    });

    // --- init ---
    renderMenu();
    renderHistory();
    savePoints(loadPoints());

    activeOrder = loadActiveOrder();
    if(activeOrder){
      // If they refresh mid-order, show last known status (timers won't continue)
      toast("Restored active order from this phone");
    }
    updateTotal();
    renderStatus();
  </script>
</body>
</html>
