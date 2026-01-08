<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8"/>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>CookVibe™ Demo</title>
  <meta name="robots" content="noindex, nofollow"/>

  <style>
    *{box-sizing:border-box;font-family:Arial,sans-serif}
    body{margin:0;background:#0f172a;color:#fff}
    .container{max-width:1050px;margin:auto;padding:20px}
    header{text-align:center;margin-bottom:18px}
    .subtitle{color:#94a3b8;margin-top:6px}
    h1,h2,h3{margin:0 0 10px 0}
    h4{margin:0 0 8px 0}
    input,textarea,select{width:100%;padding:10px;border-radius:10px;border:none;margin-bottom:10px}
    textarea{min-height:88px}
    button{padding:10px 16px;border-radius:999px;border:none;background:#22c55e;color:#000;font-weight:800;cursor:pointer}
    button:hover{opacity:.92}
    button.secondary{background:#fbbf24;color:#000}
    button.ghost{background:transparent;color:#fff;border:1px solid #334155}
    button.disabled{opacity:.45;cursor:not-allowed}
    .error{color:#f87171;margin:8px 0 0 0}
    .hidden{display:none}
    .nav{display:flex;justify-content:space-between;align-items:center;margin:14px 0 14px 0}
    .badge{background:#334155;padding:4px 10px;border-radius:12px;font-size:12px}
    .grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(300px,1fr));gap:14px}
    .card{background:#1e293b;padding:16px;border-radius:18px;border:1px solid #334155}
    .muted{color:#94a3b8}
    .tiny{color:#94a3b8;font-size:12px;line-height:1.35}
    hr{border:none;border-top:1px solid #334155;margin:14px 0}

    .pill{padding:4px 10px;border-radius:999px;font-size:12px;font-weight:900;letter-spacing:.4px}
    .pill[data-state="available"]{background:#22c55e;color:#000}
    .pill[data-state="unavailable"]{background:#f87171;color:#000}

    .row{display:flex;gap:10px;flex-wrap:wrap;align-items:center}
    .votes{display:flex;gap:10px;align-items:center;justify-content:space-between}
    .voteBtn{padding:8px 12px;border-radius:999px;border:1px solid #334155;background:transparent;color:#fff;font-weight:800}
    .voteBtn:hover{opacity:.9}

    /* Modal */
    .modal{position:fixed;inset:0;background:rgba(0,0,0,.65);display:flex;align-items:center;justify-content:center;padding:18px;z-index:999}
    .modalCard{background:#0b1224;border:1px solid #334155;border-radius:16px;max-width:600px;width:100%;padding:16px}
    .modalHeader{display:flex;align-items:center;justify-content:space-between;gap:10px}

    /* Netlify Forms: keep hidden but present */
    form[netlify]{display:none}
  </style>
</head>

<body>
  <div class="container">
    <header>
      <h1>CookVibe™ Demo</h1>
      <p class="subtitle">Private beta demo (User view + Creator view)</p>
    </header>

    <!-- ACCESS -->
    <section id="access" class="card">
      <h2 style="margin:0 0 6px 0;">Enter Access Code</h2>
      <p class="muted" style="margin:0 0 10px 0;">
        Use a code provided by the team. Creator codes unlock creator-only tools.
      </p>
      <input id="codeInput" placeholder="Enter access code"/>
      <button id="enterBtn">Enter Demo</button>
      <p id="error" class="error"></p>

      <div class="row" style="margin-top:10px;">
        <span class="badge">User codes</span>
        <span class="tiny">USERBETA, COOKVIBEUSER</span>
      </div>
      <div class="row" style="margin-top:8px;">
        <span class="badge">Creator codes</span>
        <span class="tiny">CREATORBETA, SHAUNCREATOR</span>
      </div>

      <p class="tiny" style="margin-top:10px;">
        Tip: When deployed on Netlify, enable Password Protection at the site level for an extra layer of control.
      </p>
    </section>

    <!-- DEMO -->
    <section id="demo" class="hidden">
      <nav class="nav">
        <span style="font-weight:900;">🍳 CookVibe</span>
        <span id="roleBadge" class="badge">ROLE: USER</span>
      </nav>

      <div class="grid">
        <div class="card">
          <h3>Creator Page (Preview)</h3>
          <p style="margin:0;"><b>Name:</b> Demo Creator</p>
          <p style="margin:6px 0 0 0;"><b>Country:</b> United States</p>
          <p style="margin:6px 0 0 0;"><b>Language:</b> English</p>

          <hr/>
          <p class="muted" style="margin:0;"><b>Follow CTA:</b> Follow for more recipes</p>
          <button class="secondary" style="margin-top:10px;">➕ Follow Creator</button>

          <p class="tiny" style="margin-top:10px;">
            Demo note: Mobile app includes TikTok-style feed + live stream. Web demo focuses on flows.
          </p>
        </div>

        <div class="card">
          <h3>Recipe Vault (Rolodex)</h3>
          <ul style="margin:0 0 6px 18px;">
            <li>Spicy Garlic Shrimp</li>
            <li>Heart-Healthy Bowl</li>
            <li>Kidney-Friendly Veggie Plate</li>
          </ul>
          <p class="tiny">
            Creators store recipes on their page in a categorized vault. Searchable by all users.
          </p>
        </div>

        <!-- ORDER + FALLBACK -->
        <div class="card">
          <h3>Order Locally (Referral Model)</h3>

          <div class="row" style="margin-bottom:10px;">
            <span id="dishStatusPill" class="pill" data-state="available">AVAILABLE</span>
            <span class="muted">Dish: <b id="dishNameText">Spicy Garlic Shrimp</b></span>
          </div>

          <p id="dishReasonText" style="color:#fbbf24;margin:0 0 10px 0;"></p>

          <div class="row">
            <button id="orderBtn">🍽 Order This Dish Near You</button>
            <button id="fallbackBtn" class="secondary">🔎 Find Similar Nearby</button>
          </div>

          <p class="tiny" style="margin-top:10px;">
            Orders are fulfilled by third-party delivery partners. CookVibe does not prepare or deliver food.
          </p>

          <!-- CREATOR-ONLY CONTROLS (NOT VISIBLE TO USERS) -->
          <div id="creatorControls" class="hidden">
            <hr/>
            <h4>Creator Controls</h4>
            <label class="tiny" style="display:block;margin-bottom:6px;">Availability</label>
            <select id="creatorAvail">
              <option value="available">Available</option>
              <option value="unavailable">Unavailable</option>
            </select>

            <label class="tiny" style="display:block;margin-bottom:6px;">Reason (optional)</label>
            <input id="creatorReason" placeholder="Sold out / Not delivering / Not available today"/>

            <button id="creatorApply" class="ghost">Apply</button>

            <p class="tiny" style="margin-top:10px;">
              Creator tools appear only in creator mode. Users never see these controls.
            </p>
          </div>
        </div>

        <div class="card">
          <h3>Leaderboard (Preview)</h3>
          <ol style="margin:0 0 6px 18px;">
            <li>🇺🇸 Top Creator — Free Annual Next Year</li>
            <li>🇺🇸 Runner Up — 50% Off Next Year</li>
            <li>🇺🇸 3rd Place — 25% Off Next Year</li>
          </ol>
          <p class="tiny">Rewards apply per country. Top creators in each country receive annual rewards.</p>
        </div>

        <div class="card">
          <h3>Feedback (All Users)</h3>
          <textarea id="feedbackText" placeholder="What feels missing, confusing, or exciting?"></textarea>
          <div class="row">
            <button id="sendFeedback">Send Feedback</button>
            <button id="exportAnalytics" class="ghost">Export Analytics</button>
          </div>
          <p class="tiny" style="margin-top:10px;">
            Demo feedback is stored locally + captured in analytics export. In production, it goes to a platform dashboard.
          </p>
        </div>

        <!-- CREATOR-ONLY: SUGGESTIONS + VOTING + GROUPING + EMAIL -->
        <div id="creatorOnlyPanel" class="card hidden">
          <div class="row" style="justify-content:space-between;">
            <h3 style="margin:0;">Creator Suggestions (Private)</h3>
            <span class="badge">CREATORS ONLY</span>
          </div>

          <p class="tiny" style="margin-top:10px;">
            This section is invisible to users. Use it to propose features, vote on ideas, and send a summary to the team.
          </p>

          <hr/>

          <!-- 1) SUGGESTION BOX -->
          <h4>Submit a Suggestion</h4>
          <textarea id="creatorSuggestionText" placeholder="What feature would help you earn more or create better content?"></textarea>
          <div class="row">
            <button id="sendCreatorSuggestion">Submit Suggestion</button>
            <button id="emailCreatorSummary" class="ghost">Email Summary</button>
          </div>
          <p class="tiny" style="margin-top:10px;">
            Email uses your device’s mail app (no backend). If deployed on Netlify, we can also capture suggestions via Netlify Forms.
          </p>

          <hr/>

          <!-- 2) FEATURE VOTING -->
          <h4>Feature Voting</h4>
          <p class="tiny" style="margin-top:0;">Vote on what matters most for creators. Top items rise automatically.</p>

          <div id="voteList" style="display:grid;gap:10px;"></div>

          <hr/>

          <!-- 3) TOP REQUESTED + 4) AUTO GROUPING -->
          <h4>Top Requested + Auto Grouping</h4>
          <div class="row" style="align-items:flex-start;">
            <div style="flex:1;min-width:260px;">
              <p class="tiny" style="margin:0 0 8px 0;"><b>Top Requested (from suggestions + votes)</b></p>
              <div id="topRequested" class="tiny"></div>
            </div>
            <div style="flex:1;min-width:260px;">
              <p class="tiny" style="margin:0 0 8px 0;"><b>Grouped Themes</b></p>
              <div id="groupedThemes" class="tiny"></div>
            </div>
          </div>

          <p class="tiny" style="margin-top:10px;">
            Themes are auto-tagged by keywords (Monetization, Editing, Delivery, Translation, Live, Recipes, Analytics, Other).
          </p>
        </div>
      </div>

      <footer style="text-align:center;margin-top:26px;color:#94a3b8">
        Founded by <b>Shaun Wint</b> • CookVibe™
      </footer>
    </section>
  </div>

  <!-- Order Modal -->
  <div id="orderModal" class="modal hidden">
    <div class="modalCard">
      <div class="modalHeader">
        <h3 style="margin:0;">Order This Dish Near You</h3>
        <button id="orderClose" class="ghost">✕</button>
      </div>

      <p class="muted" style="margin:10px 0 10px 0;">
        Enter ZIP code or city. We’ll open a delivery partner search.
      </p>

      <input id="orderLocation" placeholder="ZIP code or city"/>
      <button id="orderSetLocation">Continue</button>

      <div id="orderPartnerButtons" class="hidden" style="margin-top:12px;">
        <div class="row">
          <button id="orderDoorDash">DoorDash</button>
          <button id="orderUberEats">Uber Eats</button>
        </div>
      </div>

      <p class="tiny" style="margin-top:12px;">
        You’re ordering through a third-party partner. Availability, pricing, and delivery are handled by the provider.
      </p>
    </div>
  </div>

  <!-- Fallback Modal -->
  <div id="fallbackModal" class="modal hidden">
    <div class="modalCard">
      <div class="modalHeader">
        <h3 style="margin:0;">Find Similar Nearby</h3>
        <button id="fallbackClose" class="ghost">✕</button>
      </div>

      <p class="muted" style="margin:10px 0 10px 0;">
        We’ll search delivery partners first. If needed, you can open a Maps search.
      </p>

      <input id="fallbackLocation" placeholder="ZIP code or city"/>
      <button id="fallbackSetLocation">Continue</button>

      <div id="fallbackPartnerButtons" class="hidden" style="margin-top:12px;">
        <div class="row">
          <button id="fallbackDoorDash">DoorDash</button>
          <button id="fallbackUberEats">Uber Eats</button>
        </div>
      </div>

      <div id="fallbackMapsButton" class="hidden" style="margin-top:10px;">
        <button id="fallbackMaps" class="ghost">Open Maps Search</button>
      </div>

      <p class="tiny" style="margin-top:12px;">
        Results provided by third parties. CookVibe does not prepare or deliver food.
      </p>
    </div>
  </div>

  <!-- OPTIONAL: Netlify Forms capture (works only when deployed on Netlify) -->
  <form name="creator-suggestions" method="POST" data-netlify="true" netlify>
    <input type="hidden" name="form-name" value="creator-suggestions" />
    <input type="text" name="creator_id" />
    <textarea name="suggestion"></textarea>
    <textarea name="summary_json"></textarea>
  </form>

  <script>
    // ===== Role-based Demo with Creator-only Panels =====
    const USER_CODES = ["USERBETA", "COOKVIBEUSER"];
    const CREATOR_CODES = ["CREATORBETA", "SHAUNCREATOR"];

    const CREATOR_ID = "demo_creator_001";
    const DISH_NAME = "Spicy Garlic Shrimp";
    const DEFAULT_COUNTRY = "United States";

    function qs(id){ return document.getElementById(id); }

    // ---- Analytics (MVP) ----
    function getEvents() {
      try { return JSON.parse(localStorage.getItem("cv_events") || "[]"); }
      catch { return []; }
    }
    function track(event, props = {}) {
      const payload = { event, props, ts: new Date().toISOString() };
      const events = getEvents();
      events.push(payload);
      localStorage.setItem("cv_events", JSON.stringify(events));
      console.log("[CookVibe analytics]", payload);
    }
    function exportAnalytics() {
      const blob = new Blob([JSON.stringify(getEvents(), null, 2)], { type: "application/json" });
      const a = document.createElement("a");
      a.href = URL.createObjectURL(blob);
      a.download = "cookvibe_demo_analytics.json";
      a.click();
      URL.revokeObjectURL(a.href);
    }

    // ---- Dish availability (MVP) ----
    function getDishStatus() { return localStorage.getItem("cv_dish_status") || "available"; }
    function setDishStatus(status) { localStorage.setItem("cv_dish_status", status); }
    function getDishReason() { return localStorage.getItem("cv_dish_reason") || ""; }
    function setDishReason(reason) { localStorage.setItem("cv_dish_reason", reason); }

    // ---- Creator Suggestions + Voting storage ----
    function getCreatorSuggestions() {
      try { return JSON.parse(localStorage.getItem("cv_creator_suggestions") || "[]"); }
      catch { return []; }
    }
    function saveCreatorSuggestions(list) {
      localStorage.setItem("cv_creator_suggestions", JSON.stringify(list));
    }

    function getVoteState() {
      try { return JSON.parse(localStorage.getItem("cv_feature_votes") || "{}"); }
      catch { return {}; }
    }
    function saveVoteState(v) {
      localStorage.setItem("cv_feature_votes", JSON.stringify(v));
    }

    // ---- Modals ----
    function openModal(id){ qs(id).classList.remove("hidden"); }
    function closeModal(id){ qs(id).classList.add("hidden"); }

    // ---- Partner URLs (placeholders) ----
    function partnerSearchUrl(partner, query, location) {
      const q = encodeURIComponent(`${query} ${location}`.trim());
      if (partner === "doordash") return `https://www.doordash.com/search/store/${q}/`;
      if (partner === "ubereats")  return `https://www.ubereats.com/search?q=${q}`;
      return "#";
    }
    function mapsSearchUrl(query, location) {
      const q = encodeURIComponent(`${query} near ${location}`.trim());
      return `https://maps.apple.com/?q=${q}`;
    }

    // ---- Role control ----
    let ROLE = "USER"; // USER or CREATOR

    function setRole(newRole) {
      ROLE = newRole;
      qs("roleBadge").textContent = `ROLE: ${ROLE}`;
      // Creator-only panels
      if (ROLE === "CREATOR") {
        qs("creatorOnlyPanel").classList.remove("hidden");
        qs("creatorControls").classList.remove("hidden");
      } else {
        qs("creatorOnlyPanel").classList.add("hidden");
        qs("creatorControls").classList.add("hidden");
      }
      track("role_set", { role: ROLE });
      // Render creator-only content if applicable
      if (ROLE === "CREATOR") {
        renderVoteList();
        renderTopAndGroups();
      }
    }

    // ---- Render order section ----
    function renderOrderSection() {
      const status = getDishStatus();
      const reason = getDishReason();

      const orderBtn = qs("orderBtn");
      const statusPill = qs("dishStatusPill");
      const reasonText = qs("dishReasonText");

      qs("dishNameText").textContent = DISH_NAME;

      if (status === "available") {
        statusPill.textContent = "AVAILABLE";
        statusPill.dataset.state = "available";
        reasonText.textContent = "";
        orderBtn.disabled = false;
        orderBtn.classList.remove("disabled");
      } else {
        statusPill.textContent = "UNAVAILABLE";
        statusPill.dataset.state = "unavailable";
        orderBtn.disabled = true;
        orderBtn.classList.add("disabled");
        reasonText.textContent = reason ? `Reason: ${reason}` : "Reason: Unavailable";
        track("order_unavailable_shown", { creator_id: CREATOR_ID, dish: DISH_NAME, reason: reason || "unavailable" });
      }
    }

    // ---- Access ----
    function enterDemo(){
      const code = qs("codeInput").value.trim().toUpperCase();

      if (CREATOR_CODES.includes(code)) {
        qs("access").style.display="none";
        qs("demo").classList.remove("hidden");
        setRole("CREATOR");
        track("demo_entered", { role:"CREATOR", creator_id: CREATOR_ID, country: DEFAULT_COUNTRY });
        renderOrderSection();
        return;
      }

      if (USER_CODES.includes(code)) {
        qs("access").style.display="none";
        qs("demo").classList.remove("hidden");
        setRole("USER");
        track("demo_entered", { role:"USER", country: DEFAULT_COUNTRY });
        renderOrderSection();
        return;
      }

      qs("error").innerText = "Invalid access code.";
    }

    // ---- Order/Fallback actions ----
    function openOrderModal() {
      if (getDishStatus() !== "available") return;
      track("order_click", { dish: DISH_NAME, role: ROLE });
      qs("orderPartnerButtons").classList.add("hidden");
      qs("orderLocation").value = "";
      openModal("orderModal");
    }
    function openFallbackModal() {
      track("fallback_opened", { dish: DISH_NAME, role: ROLE });
      qs("fallbackPartnerButtons").classList.add("hidden");
      qs("fallbackMapsButton").classList.add("hidden");
      qs("fallbackLocation").value = "";
      openModal("fallbackModal");
    }

    function submitLocation(modalType) {
      const loc = (modalType === "order") ? qs("orderLocation").value.trim() : qs("fallbackLocation").value.trim();
      if (!loc) { alert("Please enter ZIP code or city."); return; }
      track("location_entered", { modal: modalType, role: ROLE, location_len: loc.length });

      if (modalType === "order") {
        qs("orderPartnerButtons").classList.remove("hidden");
      } else {
        qs("fallbackPartnerButtons").classList.remove("hidden");
        qs("fallbackMapsButton").classList.remove("hidden");
      }
    }

    function goPartner(partner, modalType) {
      const loc = (modalType === "order") ? qs("orderLocation").value.trim() : qs("fallbackLocation").value.trim();
      const url = partnerSearchUrl(partner, DISH_NAME, loc);
      track("partner_selected", { partner, modal: modalType, role: ROLE, dish: DISH_NAME });
      window.open(url, "_blank");
    }

    function goMapsFallback() {
      const loc = qs("fallbackLocation").value.trim();
      const url = mapsSearchUrl(DISH_NAME, loc);
      track("maps_fallback_selected", { role: ROLE, dish: DISH_NAME });
      window.open(url, "_blank");
    }

    // ---- Creator availability controls ----
    function applyCreatorAvailability() {
      if (ROLE !== "CREATOR") return;
      const status = qs("creatorAvail").value;
      const reason = qs("creatorReason").value.trim();
      setDishStatus(status);
      setDishReason(reason);
      track("creator_toggle_availability", { creator_id: CREATOR_ID, dish: DISH_NAME, status, reason });
      renderOrderSection();
    }

    // ---- Feedback (all users) ----
    function sendFeedback() {
      const text = qs("feedbackText").value.trim();
      track("feedback_submitted", { role: ROLE, length: text.length });
      alert("Feedback saved (demo). Thank you!");
      qs("feedbackText").value = "";
    }

    // ===== Creator-only Upgrades 1–4 =====
    // 1) Feature Voting
    const DEFAULT_FEATURES = [
      "Better earnings dashboard + payout transparency",
      "In-app video editor (yearly subscribers)",
      "Real-time translation subtitles",
      "Live cooking with paid access (monthly) / free on annual",
      "Order locally integration + fallback search",
      "Recipe Vault categories + meal plans",
      "Creator storefront + merch integration",
      "Country-based leaderboards + rewards"
    ];

    function renderVoteList() {
      if (ROLE !== "CREATOR") return;

      const votes = getVoteState();
      // Initialize defaults if empty
      DEFAULT_FEATURES.forEach(f => { if (votes[f] == null) votes[f] = 0; });
      saveVoteState(votes);

      const list = qs("voteList");
      list.innerHTML = "";

      // Sort by vote count desc
      const items = Object.entries(votes).sort((a,b)=>b[1]-a[1]);

      items.forEach(([feature, count]) => {
        const row = document.createElement("div");
        row.className = "card";
        row.style.background = "#0b1224";
        row.style.borderColor = "#334155";
        row.style.borderRadius = "14px";
        row.style.padding = "12px";

        row.innerHTML = `
          <div class="votes">
            <div style="flex:1;">
              <div style="font-weight:800;">${escapeHtml(feature)}</div>
              <div class="tiny">Votes: <b>${count}</b></div>
            </div>
            <button class="voteBtn" data-feature="${escapeAttr(feature)}">▲ Vote</button>
          </div>
        `;

        list.appendChild(row);
      });

      // Attach vote handlers
      list.querySelectorAll(".voteBtn").forEach(btn => {
        btn.addEventListener("click", () => {
          const f = btn.getAttribute("data-feature");
          const v = getVoteState();
          v[f] = (v[f] || 0) + 1;
          saveVoteState(v);
          track("creator_feature_voted", { creator_id: CREATOR_ID, feature: f });
          renderVoteList();
          renderTopAndGroups();
        });
      });
    }

    // 2) Top Requested + 3) Auto Grouping
    function tagSuggestion(text) {
      const t = (text || "").toLowerCase();
      const rules = [
        ["Monetization", ["earn","payout","money","subscription","revenue","split","commission"]],
        ["Editing", ["edit","editor","trim","effects","music","caption"]],
        ["Delivery", ["deliver","order","doordash","uber","pickup","local"]],
        ["Translation", ["translate","subtitle","language","captioning"]],
        ["Live", ["live","stream","livestream"]],
        ["Recipes", ["recipe","vault","rolodex","category","meal plan","ingredients"]],
        ["Analytics", ["analytics","stats","views","conversion","tracking"]],
      ];
      for (const [tag, keys] of rules) {
        if (keys.some(k => t.includes(k))) return tag;
      }
      return "Other";
    }

    function getTopRequestedData() {
      const suggestions = getCreatorSuggestions();
      const votes = getVoteState();

      // count suggestion themes
      const themeCounts = {};
      suggestions.forEach(s => {
        const tag = tagSuggestion(s.suggestion);
        themeCounts[tag] = (themeCounts[tag] || 0) + 1;
      });

      // combine “top requested” from votes + suggestions
      const topVotes = Object.entries(votes).sort((a,b)=>b[1]-a[1]).slice(0,5);
      const topThemes = Object.entries(themeCounts).sort((a,b)=>b[1]-a[1]);

      return { topVotes, topThemes, suggestionsCount: suggestions.length };
    }

    function renderTopAndGroups() {
      if (ROLE !== "CREATOR") return;

      const { topVotes, topThemes, suggestionsCount } = getTopRequestedData();

      const topDiv = qs("topRequested");
      const groupDiv = qs("groupedThemes");

      topDiv.innerHTML = `
        <div class="badge" style="display:inline-block;margin-bottom:8px;">Suggestions: ${suggestionsCount}</div>
        ${topVotes.length ? topVotes.map(([f,c],i)=>`<div>• <b>${i+1}.</b> ${escapeHtml(f)} <span class="muted">(votes: ${c})</span></div>`).join("") : "<div class='muted'>No votes yet.</div>"}
      `;

      groupDiv.innerHTML = topThemes.length
        ? topThemes.map(([tag,count])=>`<div>• <b>${escapeHtml(tag)}:</b> ${count}</div>`).join("")
        : "<div class='muted'>No suggestions yet.</div>";
    }

    // 4) Email Delivery (no backend)
    function emailCreatorSummary() {
      if (ROLE !== "CREATOR") return;

      const suggestions = getCreatorSuggestions();
      const votes = getVoteState();
      const summary = getTopRequestedData();

      const bodyObj = {
        creator_id: CREATOR_ID,
        created_at: new Date().toISOString(),
        top_votes: summary.topVotes,
        grouped_themes: summary.topThemes,
        suggestions: suggestions.slice(-25) // last 25
      };

      const subject = encodeURIComponent("CookVibe Creator Suggestions Summary (Demo)");
      const body = encodeURIComponent(JSON.stringify(bodyObj, null, 2));

      // Opens Mail app with content (works on iPhone)
      window.location.href = `mailto:?subject=${subject}&body=${body}`;

      track("creator_summary_emailed", { creator_id: CREATOR_ID, suggestions: suggestions.length });
    }

    // Submit creator suggestion (creator only) + optional Netlify capture
    async function submitCreatorSuggestion() {
      if (ROLE !== "CREATOR") return;

      const text = qs("creatorSuggestionText").value.trim();
      if (!text) { alert("Please enter a suggestion."); return; }

      const list = getCreatorSuggestions();
      list.push({ creator_id: CREATOR_ID, suggestion: text, tag: tagSuggestion(text), ts: new Date().toISOString() });
      saveCreatorSuggestions(list);

      track("creator_suggestion_submitted", { creator_id: CREATOR_ID, length: text.length, tag: tagSuggestion(text) });

      // Optional Netlify Forms capture (works if deployed on Netlify)
      try {
        const formData = new URLSearchParams();
        formData.append("form-name", "creator-suggestions");
        formData.append("creator_id", CREATOR_ID);
        formData.append("suggestion", text);
        formData.append("summary_json", JSON.stringify(getTopRequestedData()));

        // Netlify accepts POST to current path
        await fetch("/", {
          method: "POST",
          headers: { "Content-Type": "application/x-www-form-urlencoded" },
          body: formData.toString()
        });
      } catch (e) {
        // If not on Netlify, ignore—local storage + email still works
      }

      qs("creatorSuggestionText").value = "";
      alert("Suggestion saved. Thank you!");
      renderTopAndGroups();
    }

    // ---- Utils ----
    function escapeHtml(str){
      return String(str)
        .replaceAll("&","&amp;").replaceAll("<","&lt;").replaceAll(">","&gt;")
        .replaceAll('"',"&quot;").replaceAll("'","&#039;");
    }
    function escapeAttr(str){
      return escapeHtml(str).replaceAll("\n"," ").replaceAll("\r"," ");
    }

    // ---- Init ----
    window.addEventListener("DOMContentLoaded", () => {
      qs("enterBtn").addEventListener("click", enterDemo);

      qs("orderBtn").addEventListener("click", () => {
        if (getDishStatus() !== "available") return;
        qs("orderPartnerButtons").classList.add("hidden");
        qs("orderLocation").value = "";
        openModal("orderModal");
      });
      qs("fallbackBtn").addEventListener("click", () => {
        qs("fallbackPartnerButtons").classList.add("hidden");
        qs("fallbackMapsButton").classList.add("hidden");
        qs("fallbackLocation").value = "";
        openModal("fallbackModal");
      });

      qs("orderClose").addEventListener("click", () => closeModal("orderModal"));
      qs("fallbackClose").addEventListener("click", () => closeModal("fallbackModal"));

      qs("orderSetLocation").addEventListener("click", () => submitLocation("order"));
      qs("fallbackSetLocation").addEventListener("click", () => submitLocation("fallback"));

      qs("orderDoorDash").addEventListener("click", () => goPartner("doordash", "order"));
      qs("orderUberEats").addEventListener("click", () => goPartner("ubereats", "order"));

      qs("fallbackDoorDash").addEventListener("click", () => goPartner("doordash", "fallback"));
      qs("fallbackUberEats").addEventListener("click", () => goPartner("ubereats", "fallback"));
      qs("fallbackMaps").addEventListener("click", goMapsFallback);

      qs("sendFeedback").addEventListener("click", sendFeedback);
      qs("exportAnalytics").addEventListener("click", exportAnalytics);

      // Creator-only wires (safe even if hidden)
      qs("creatorApply").addEventListener("click", applyCreatorAvailability);
      qs("sendCreatorSuggestion").addEventListener("click", submitCreatorSuggestion);
      qs("emailCreatorSummary").addEventListener("click", emailCreatorSummary);

      // initial render
      renderOrderSection();
    });
  </script>
</body>
</html>
