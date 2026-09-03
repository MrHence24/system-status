<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<title>System Status</title>
<style>
:root {
  --bg: #0f0f10;
  --card: #1c1c1e;
  --card2: #2c2c2e;
  --text: #ffffff;
  --muted: #a1a1a6;
  --red: #ff453a;
}
* {
  box-sizing: border-box;
}
body {
  margin: 0;
  background: var(--bg);
  color: var(--text);
  font-family: -apple-system, BlinkMacSystemFont, sans-serif;
}
header {
  padding: 18px 20px 10px;
  text-align: center;
}
h1 {
  margin: 0;
  font-size: 28px;
}
.subtitle {
  margin-top: 5px;
  color: var(--muted);
  font-size: 14px;
}
/* ---------------- NAV ---------------- */
nav {
  display: flex;
  gap: 8px;
  padding: 12px;
  position: sticky;
  top: 0;
  background: var(--bg);
  z-index: 10;
}
.nav-button {
  flex: 1;
  padding: 13px 5px;
  border: none;
  border-radius: 14px;
  background: var(--card2);
  color: white;
  font-size: 14px;
  font-weight: 600;
}
.nav-button.active {
  background: white;
  color: black;
}
/* ---------------- PAGES ---------------- */
.page {
  display: none;
  padding: 8px 16px 35px;
}
.page.active {
  display: block;
}
/* ---------------- STATUS ---------------- */
.section-title {
  font-size: 13px;
  text-transform: uppercase;
  letter-spacing: 1px;
  color: var(--muted);
  margin: 22px 5px 10px;
}
.status {
  background: var(--card);
  border-radius: 18px;
  padding: 16px;
  margin-bottom: 12px;
}
.status-name {
  font-size: 18px;
  font-weight: 650;
}
.status-description {
  font-size: 13px;
  color: var(--muted);
  margin: 5px 0 14px;
}
.levels {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 6px;
}
.level {
  border: 1px solid #48484a;
  background: var(--card2);
  color: white;
  border-radius: 10px;
  padding: 11px 2px;
  font-size: 17px;
  font-weight: bold;
}
.level.selected {
  background: white;
  color: black;
}
.level-label {
  display: block;
  font-size: 8px;
  margin-top: 4px;
  font-weight: normal;
}
/* ---------------- TRANSLATION ---------------- */
#translation {
  background: var(--card);
  border-radius: 20px;
  padding: 20px;
  margin-top: 25px;
}
.system-state {
  font-size: 24px;
  font-weight: 800;
  margin-bottom: 10px;
}
.best-response {
  background: var(--card2);
  padding: 15px;
  border-radius: 14px;
  margin: 15px 0;
  font-size: 18px;
  font-weight: bold;
}
.translation-section {
  margin-top: 20px;
}
.translation-section h3 {
  margin-bottom: 8px;
}
.translation-section p,
.translation-section li {
  line-height: 1.5;
  color: #dedee2;
}
/* ---------------- QUICK COMMUNICATE ---------------- */
.quick-intro {
  color: var(--muted);
  line-height: 1.4;
  margin-bottom: 18px;
}
.quick-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 12px;
}
.quick-button {
  min-height: 125px;
  border: none;
  border-radius: 22px;
  padding: 15px 8px;
  color: white;
  background: var(--card);
  font-size: 17px;
  font-weight: 700;
}
.quick-icon {
  display: block;
  font-size: 36px;
  margin-bottom: 8px;
}
/* ---------------- MESSAGE SCREEN ---------------- */
.message-screen {
  min-height: 80vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
}
.message-icon {
  font-size: 75px;
}
.message-title {
  font-size: 32px;
  font-weight: 800;
  margin: 18px 0;
}
.message-text {
  font-size: 20px;
  line-height: 1.5;
  color: #ddd;
}
.back-button {
  margin-top: 35px;
  padding: 16px;
  border: none;
  border-radius: 16px;
  font-size: 18px;
}
/* ---------------- RED ALERT ---------------- */
.alert-button {
  width: 100%;
  background: var(--red);
  border: none;
  color: white;
  border-radius: 22px;
  padding: 22px;
  font-size: 21px;
  font-weight: 900;
  margin-bottom: 20px;
}
.alert-box {
  background: #321616;
  border: 2px solid var(--red);
  border-radius: 22px;
  padding: 22px;
  margin-top: 20px;
}
.alert-box h2 {
  margin-top: 0;
  color: var(--red);
}
.dismiss {
  width: 100%;
  padding: 15px;
  border-radius: 14px;
  border: none;
  margin-top: 15px;
  font-size: 16px;
}
</style>
</head>
<body>
<header>
  <h1>🧠 System Status</h1>
  <div class="subtitle">
    Real-time accessibility & communication
  </div>
</header>
<nav>

⚡ Quick
📊 Status
🚨 Alert
</nav>
<!-- ================= QUICK ================= -->
<div id="quick" class="page active">
  <div class="quick-intro">
Tap once. The app will communicate for you.
  </div>
  <div class="quick-grid">
<button class="quick-button"
  onclick="showMessage('lessTalking')">
  <span class="quick-icon">🔇</span>
  Less Talking
</button>
<button class="quick-button"
  onclick="showMessage('break')">
  <span class="quick-icon">🧘</span>
  I Need a Break
</button>
<button class="quick-button"
  onclick="showMessage('sensory')">
  <span class="quick-icon">🔊</span>
  Too Much Input
</button>
<button class="quick-button"
  onclick="showMessage('demands')">
  <span class="quick-icon">🛑</span>
  Reduce Demands
</button>
<button class="quick-button"
  onclick="showMessage('understand')">
  <span class="quick-icon">💬</span>
  I Understand
</button>
<button class="quick-button"
  onclick="showMessage('notAngry')">
  <span class="quick-icon">❤️</span>
  Not Angry
</button>
<button class="quick-button"
  onclick="showMessage('time')">
  <span class="quick-icon">⏳</span>
  Give Me Time
</button>
<button class="quick-button"
  onclick="showMessage('stim')">
  <span class="quick-icon">🧠</span>
  I Need to Stim
</button>
  </div>
</div>
<!-- ================= STATUS ================= -->
<div id="status" class="page">
  <div id="status-app"></div>
  <div id="translation">
<h2>Translation</h2>
<div id="translation-content"></div>
  </div>
</div>
<!-- ================= ALERT ================= -->
<div id="alert" class="page">
🚨 RED ALERT
<br>
TOO OVERLOADED TO EXPLAIN
  </button>
  <div id="alert-content"></div>
</div>
<!-- ================= MESSAGE SCREEN ================= -->
<div id="message" class="page"></div>
<script>
/* =========================================
   NAVIGATION
========================================= */
function showPage(pageId, button) {
  document
    .querySelectorAll('.page')
    .forEach(page =>
      page.classList.remove('active')
    );
  document
    .getElementById(pageId)
    .classList.add('active');
  document
    .querySelectorAll('.nav-button')
    .forEach(btn =>
      btn.classList.remove('active')
    );
  if (button) {
    button.classList.add('active');
  }
}
/* =========================================
   QUICK COMMUNICATION MESSAGES
========================================= */
const messages = {
  lessTalking: {
    icon: "🔇",
    title: "I NEED LESS TALKING",
    text:
      "I am having difficulty processing and responding to conversation right now. Please reduce unnecessary questions and give me time to process. I may understand what you are saying even if I cannot respond normally."
  },
  break: {
    icon: "🧘",
    title: "I NEED A BREAK",
    text:
      "My current capacity is reduced and I need time away from demands or stimulation. Please allow me to take a break without requiring me to explain or justify it."
  },
  sensory: {
    icon: "🔊",
    title: "TOO MUCH INPUT",
    text:
      "My nervous system is receiving more sensory input than I can comfortably process right now. Reducing noise, talking, interruptions, light, touch, or other stimulation would help."
  },
  demands: {
    icon: "🛑",
    title: "PLEASE REDUCE DEMANDS",
    text:
      "Additional requests or expectations are difficult for me to process right now. Please avoid adding unnecessary demands and focus on what is actually urgent."
  },
  understand: {
    icon: "💬",
    title: "I UNDERSTAND",
    text:
      "I may understand what you are saying even though I am having difficulty responding. Please do not assume silence or delayed communication means I am ignoring you."
  },
  notAngry: {
    icon: "❤️",
    title: "I'M NOT ANGRY",
    text:
      "My reduced communication, facial expression, withdrawal, or need for space does not necessarily mean I am angry or upset with you. I currently have limited capacity to interact."
  },
  time: {
    icon: "⏳",
    title: "PLEASE GIVE ME TIME",
    text:
      "I need additional time to process what is happening and determine how to respond. Please avoid repeatedly asking for an immediate answer."
  },
  stim: {
    icon: "🧠",
    title: "I NEED TO STIM",
    text:
      "I may need repetitive movement, sounds, fidgeting, pacing, or another form of self-regulation. Please allow this unless there is a genuine safety concern. Stimming may help me regulate and recover capacity."
  }
};
function showMessage(key) {
  const message = messages[key];
  const page =
    document.getElementById("message");
  page.innerHTML = `
    <div class="message-screen">
      <div class="message-icon">
        ${message.icon}
      </div>
      <div class="message-title">
        ${message.title}
      </div>
      <div class="message-text">
        ${message.text}
      </div>
      <button class="back-button"
        onclick="returnToQuick()">
        ← Back
      </button>
    </div>
  `;
  showPage("message");
}
function returnToQuick() {
  document
    .querySelectorAll('.page')
    .forEach(page =>
      page.classList.remove('active')
    );
  document
    .getElementById('quick')
    .classList.add('active');
  document
    .querySelectorAll('.nav-button')
    .forEach(btn =>
      btn.classList.remove('active')
    );
  document
    .querySelector('.nav-button')
    .classList.add('active');
}
/* =========================================
   RED ALERT
========================================= */
function activateAlert() {
  document
    .getElementById("alert-content")
    .innerHTML = `
      <div class="alert-box">
        <h2>
          🚨 SYSTEM OVERLOADED
        </h2>
        <p>
          I am currently too overloaded to explain,
          answer questions, or accurately assess what
          is happening.
        </p>
        <p>
          Please do not interpret silence, delayed
          responses, reduced communication, stimming,
          withdrawal, or a need to leave as anger,
          disrespect, or lack of care.
        </p>
        <p>
          <strong>
            BEST RESPONSE:
          </strong>
          Reduce demands and sensory input. Avoid
          asking multiple questions. Allow me to take
          a break, stim, or have space.
        </p>
        <p>
          If something is urgent, communicate it
          simply and directly.
        </p>
        <button class="dismiss"
          onclick="dismissAlert()">
          I'm able to communicate again
        </button>
      </div>
    `;
}
function dismissAlert() {
  document
    .getElementById("alert-content")
    .innerHTML = "";
}
/* =========================================
   STATUS DATA
========================================= */
const metrics = {
  physical: {
    name: "🫀 Physical Capacity",
    type: "capacity",
    description: "How much can my body physically do right now?"
  },
  energy: {
    name: "⚡ Energy",
    type: "capacity",
    description: "How much usable energy do I have?"
  },
  cognitive: {
    name: "🧠 Cognitive Bandwidth",
    type: "capacity",
    description: "How much information and complexity can I process?"
  },
  executive: {
    name: "🎯 Executive Function",
    type: "capacity",
    description: "How easily can I start, organize, and complete tasks?"
  },
  communication: {
    name: "💬 Communication Capacity",
    type: "capacity",
    description: "How much communication can I produce and process?"
  },
  social: {
    name: "🤝 Social Capacity",
    type: "capacity",
    description: "How much interpersonal interaction can I handle?"
  },
  sensory: {
    name: "🔊 Sensory Load",
    type: "load",
    description: "How overloaded am I by sensory input?"
  },
  stress: {
    name: "⚠️ Stress Load",
    type: "load",
    description: "How much accumulated pressure is my system carrying?"
  },
  demand: {
    name: "📋 Demand Pressure",
    type: "load",
    description: "How difficult are expectations and requests right now?"
  },
  transition: {
    name: "🔄 Transition Difficulty",
    type: "load",
    description: "How difficult is switching tasks or changing plans?"
  }
};
const capacityLabels =
["", "Critical", "Low", "Limited", "Good", "Full"];
const loadLabels =
["", "Minimal", "Manageable", "Elevated", "High", "Critical"];
let values =
JSON.parse(
  localStorage.getItem("systemStatus")
) || {
  physical: 3,
  energy: 3,
  cognitive: 3,
  executive: 3,
  communication: 3,
  social: 3,
  sensory: 3,
  stress: 3,
  demand: 3,
  transition: 3
};
/* =========================================
   RENDER STATUS
========================================= */
function renderStatus() {
  const app =
    document.getElementById(
      "status-app"
    );
  app.innerHTML = "";
  addStatusSection(
    app,
    "Available Capacity",
    "capacity"
  );
  addStatusSection(
    app,
    "Current Load",
    "load"
  );
  updateTranslation();
}
function addStatusSection(
  app,
  title,
  type
) {
  const heading =
    document.createElement("div");
  heading.className =
    "section-title";
  heading.textContent =
    title;
  app.appendChild(
    heading
  );
  Object.entries(metrics)
    .filter(
      ([key, metric]) =>
        metric.type === type
    )
    .forEach(
      ([key, metric]) => {
        app.appendChild(
          createMetric(
            key,
            metric
          )
        );
      }
    );
}
function createMetric(
  key,
  metric
) {
  const card =
    document.createElement("div");
  card.className =
    "status";
  card.innerHTML = `
    <div class="status-name">
      ${metric.name}
    </div>
    <div class="status-description">
      ${metric.description}
    </div>
  `;
  const levels =
    document.createElement("div");
  levels.className =
    "levels";
  for (
    let level = 1;
    level <= 5;
    level++
  ) {
    const button =
      document.createElement("button");
    button.className =
      "level";
    if (
      values[key] === level
    ) {
      button.classList.add(
        "selected"
      );
    }
    const labels =
      metric.type === "capacity"
        ? capacityLabels
        : loadLabels;
    button.innerHTML =
      level +
      `<span class="level-label">
        ${labels[level]}
      </span>`;
    button.onclick =
      () => {
        values[key] =
          level;
        localStorage.setItem(
          "systemStatus",
          JSON.stringify(values)
        );
        renderStatus();
      };
    levels.appendChild(
      button
    );
  }
  card.appendChild(
    levels
  );
  return card;
}
/* =========================================
   RESPONSE-FIRST TRANSLATOR
========================================= */
function updateTranslation() {
  const capacityKeys =
    Object.keys(metrics)
      .filter(
        key =>
          metrics[key]
            .type ===
          "capacity"
      );
  const loadKeys =
    Object.keys(metrics)
      .filter(
        key =>
          metrics[key]
            .type ===
          "load"
      );
  const avgCapacity =
    capacityKeys
      .reduce(
        (
          sum,
          key
        ) =>
          sum +
          values[key],
        0
      )
    /
    capacityKeys.length;
  const avgLoad =
    loadKeys
      .reduce(
        (
          sum,
          key
        ) =>
          sum +
          values[key],
        0
      )
    /
    loadKeys.length;
  let state;
  let response;
  if (
    avgCapacity >= 4 &&
    avgLoad <= 2
  ) {
    state =
      "🟢 AVAILABLE";
    response =
      "INTERACT NORMALLY";
  }
  else if (
    avgCapacity >= 3 &&
    avgLoad <= 3
  ) {
    state =
      "🟡 LIMITED";
    response =
      "SIMPLIFY";
  }
  else if (
    avgCapacity >= 2.3
  ) {
    state =
      "🟠 STRAINED";
    response =
      "REDUCE PRESSURE";
  }
  else {
    state =
      "🔴 OVERLOADED";
    response =
      "PROTECT AND ALLOW RECOVERY";
  }
  /* DOMINANT FACTORS */
  let factors = [];
  Object.keys(metrics)
    .forEach(
      key => {
        let severity;
        if (
          metrics[key].type ===
          "capacity"
        ) {
          severity =
            6 - values[key];
        }
        else {
          severity =
            values[key];
        }
        factors.push({
          key,
          severity
        });
      }
    );
  factors.sort(
    (
      a,
      b
    ) =>
      b.severity -
      a.severity
  );
  const primary =
    factors.slice(
      0,
      3
    );
  /* WHAT IS HAPPENING */
  let cause =
    "Several factors are contributing to current capacity.";
  if (
    primary.some(
      f =>
        f.key ===
        "sensory"
    )
  ) {
    cause =
      "Sensory input is consuming a significant amount of available capacity.";
  }
  if (
    primary.some(
      f =>
        f.key ===
        "demand"
    )
  ) {
    cause +=
      " Current expectations and requests are adding additional pressure.";
  }
  if (
    primary.some(
      f =>
        f.key ===
        "executive"
    )
  ) {
    cause +=
      " Starting, organizing, or switching tasks may require extra effort.";
  }
  if (
    primary.some(
      f =>
        f.key ===
        "energy"
    )
  ) {
    cause =
      "Available energy reserves are currently limited, increasing the cost of ordinary activities.";
  }
  /* OBSERVABLE BEHAVIOR */
  let notice = [];
  if (
    values.sensory >= 4
  ) {
    notice.push(
      "Increased stimming or attempts to regulate sensory input."
    );
    notice.push(
      "A need for quiet, space, or a break."
    );
  }
  if (
    values.communication <= 2
  ) {
    notice.push(
      "Short, delayed, or absent responses."
    );
  }
  if (
    values.executive <= 2
  ) {
    notice.push(
      "Difficulty starting, organizing, or switching tasks."
    );
  }
  if (
    values.transition >= 4
  ) {
    notice.push(
      "Increased difficulty with interruptions or sudden changes."
    );
  }
  if (
    values.social <= 2
  ) {
    notice.push(
      "Withdrawal or reduced interaction."
    );
  }
  if (
    notice.length === 0
  ) {
    notice.push(
      "Normal interaction may be possible, although capacity may still be reduced."
    );
  }
  /* ACTIONS */
  let actions = [];
  if (
    response ===
    "INTERACT NORMALLY"
  ) {
    actions.push(
      "Normal conversation and expectations are generally manageable."
    );
  }
  if (
    response ===
    "SIMPLIFY"
  ) {
    actions.push(
      "Communicate clearly and avoid unnecessary complexity."
    );
    actions.push(
      "Give one request or decision at a time when possible."
    );
  }
  if (
    response ===
    "REDUCE PRESSURE"
  ) {
    actions.push(
      "Reduce unnecessary questions, decisions, and demands."
    );
    actions.push(
      "Allow a break without requiring an explanation."
    );
  }
  if (
    response ===
    "PROTECT AND ALLOW RECOVERY"
  ) {
    actions.push(
      "Reduce demands and sensory input immediately where possible."
    );
    actions.push(
      "Do not require conversation or an explanation."
    );
    actions.push(
      "Allow space, a break, and self-regulation such as stimming."
    );
  }
  /* FACTOR NAMES */
  const factorNames =
    primary
      .map(
        f =>
          metrics[f.key].name
      )
      .join(
        " • "
      );
  document
    .getElementById(
      "translation-content"
    )
    .innerHTML = `
      <div class="system-state">
        ${state}
      </div>
      <div class="best-response">
        BEST RESPONSE:
        <br>
        ${response}
      </div>
      <div class="translation-section">
        <h3>
          What is happening
        </h3>
        <p>
          ${cause}
        </p>
      </div>
      <div class="translation-section">
        <h3>
          What you may notice
        </h3>
        <ul>
          ${notice
            .map(
              item =>
                `<li>${item}</li>`
            )
            .join("")
          }
        </ul>
      </div>
      <div class="translation-section">
        <h3>
          What helps
        </h3>
        <ul>
          ${actions
            .map(
              item =>
                `<li>${item}</li>`
            )
            .join("")
          }
        </ul>
      </div>
      <div class="translation-section">
        <h3>
          Primary factors
        </h3>
        <p>
          ${factorNames}
        </p>
      </div>
    `;
}
renderStatus();
</script>
</body>
</html>
