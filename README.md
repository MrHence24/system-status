<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black">
<title>System Status</title>
<style>
:root {
  --bg: #0b0d12;
  --card: #151922;
  --card2: #202632;
  --border: #303848;
  --text: #f5f7fb;
  --muted: #a9b0bd;
  --green: #34c759;
  --yellow: #ffd60a;
  --orange: #ff9f0a;
  --red: #ff453a;
  --blue: #0a84ff;
}
* {
  box-sizing: border-box;
  -webkit-tap-highlight-color: transparent;
}
body {
  margin: 0;
  background: var(--bg);
  color: var(--text);
  font-family:
    -apple-system,
    BlinkMacSystemFont,
    "Segoe UI",
    sans-serif;
}
.app {
  max-width: 760px;
  margin: auto;
  padding: 16px;
}
header {
  text-align: center;
  padding: 10px 0 20px;
}
h1 {
  margin: 0;
  font-size: 30px;
}
.subtitle {
  margin-top: 6px;
  color: var(--muted);
  font-size: 15px;
}
.section {
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: 20px;
  padding: 16px;
  margin-bottom: 16px;
}
.section-title {
  margin: 0 0 6px;
  font-size: 19px;
}
.section-description {
  margin: 0 0 16px;
  color: var(--muted);
  font-size: 14px;
  line-height: 1.45;
}
/* RED ALERT */
.red-alert-button {
  width: 100%;
  min-height: 72px;
  border: none;
  border-radius: 18px;
  background: var(--red);
  color: white;
  font-size: 19px;
  font-weight: 800;
  cursor: pointer;
  padding: 14px;
  box-shadow:
    0 4px 18px rgba(255, 69, 58, .25);
}
.red-alert-button:active {
  transform: scale(.98);
}
.alert-panel {
  display: none;
  margin-top: 14px;
  padding: 18px;
  background: rgba(255, 69, 58, .12);
  border: 1px solid var(--red);
  border-radius: 18px;
}
.alert-panel.active {
  display: block;
}
.alert-panel h2 {
  margin-top: 0;
}
.alert-panel p {
  line-height: 1.55;
  color: #f2d7d5;
}
.dismiss-button {
  width: 100%;
  margin-top: 10px;
  padding: 14px;
  border: none;
  border-radius: 14px;
  background: var(--card2);
  color: white;
  font-size: 16px;
  font-weight: 700;
}
/* QUICK COMMUNICATION */
.quick-grid {
  display: grid;
  grid-template-columns:
    repeat(2, minmax(0, 1fr));
  gap: 10px;
}
.quick-button {
  min-height: 112px;
  border: 1px solid var(--border);
  border-radius: 18px;
  background: var(--card2);
  color: white;
  font-size: 16px;
  font-weight: 700;
  padding: 12px;
  cursor: pointer;
}
.quick-button:active {
  transform: scale(.97);
}
.quick-icon {
  display: block;
  font-size: 31px;
  margin-bottom: 8px;
}
/* STATUS */
.status-group-title {
  margin: 24px 0 10px;
  font-size: 13px;
  font-weight: 800;
  color: var(--muted);
  text-transform: uppercase;
  letter-spacing: 1px;
}
.status-group-title:first-child {
  margin-top: 0;
}
.metric {
  padding: 15px;
  margin-bottom: 10px;
  border-radius: 16px;
  background: var(--card2);
  border: 1px solid var(--border);
}
.metric-name {
  font-size: 17px;
  font-weight: 750;
}
.metric-description {
  margin-top: 4px;
  margin-bottom: 13px;
  color: var(--muted);
  font-size: 13px;
  line-height: 1.35;
}
.level-row {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 7px;
}
.level-button {
  min-height: 48px;
  border: 1px solid #3a4352;
  border-radius: 11px;
  background: #171c25;
  color: white;
  font-size: 16px;
  font-weight: 800;
  cursor: pointer;
}
.level-button:active {
  transform: scale(.95);
}
.level-button.selected {
  background: white;
  color: #101216;
  border-color: white;
}
.level-label {
  margin-top: 8px;
  text-align: center;
  color: var(--muted);
  font-size: 11px;
  min-height: 15px;
}
/* TRANSLATION */
.translation-state {
  font-size: 28px;
  font-weight: 900;
  margin-bottom: 14px;
}
.response-box {
  padding: 16px;
  margin-bottom: 18px;
  border-radius: 16px;
  background: var(--card2);
  font-size: 18px;
  font-weight: 850;
}
.response-label {
  display: block;
  margin-bottom: 5px;
  font-size: 11px;
  letter-spacing: 1px;
  color: var(--muted);
}
.translation-block {
  margin-top: 20px;
}
.translation-block h3 {
  margin: 0 0 8px;
  font-size: 16px;
}
.translation-block p,
.translation-block li {
  color: #d7dbe3;
  line-height: 1.5;
}
.translation-block ul {
  padding-left: 21px;
  margin: 8px 0;
}
/* MESSAGE OVERLAY */
.message-overlay {
  display: none;
  position: fixed;
  inset: 0;
  z-index: 100;
  padding: 22px;
  background: #0b0d12;
}
.message-overlay.active {
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
}
.message-icon {
  font-size: 76px;
}
.message-title {
  margin: 20px 0;
  font-size: 31px;
  font-weight: 900;
}
.message-text {
  font-size: 20px;
  line-height: 1.55;
  color: #e0e3e9;
}
.message-back {
  width: 100%;
  margin-top: 36px;
  padding: 17px;
  border: none;
  border-radius: 16px;
  background: white;
  color: black;
  font-size: 18px;
  font-weight: 800;
}
.footer {
  text-align: center;
  padding: 10px 0 25px;
  color: var(--muted);
  font-size: 13px;
}
@media (min-width: 650px) {
  .quick-grid {
    grid-template-columns:
      repeat(4, minmax(0, 1fr));
  }
}
</style>
</head>
<body>
<div class="app">
<header>
  <h1>🧠 System Status</h1>
  <div class="subtitle">
    Real-time accessibility & communication
  </div>
</header>
<!-- RED ALERT -->
<section class="section">
🚨 RED ALERT — TOO OVERLOADED TO EXPLAIN
  </button>
  <div
    class="alert-panel"
    id="alertPanel">
<h2>🚨 System Overloaded</h2>
<p>
  I am currently too overloaded to explain,
  answer questions, or accurately describe
  what is happening.
</p>
<p>
  Please do not interpret silence, delayed
  responses, withdrawal, stimming, or a need
  to leave as anger, disrespect, or lack of care.
</p>
<p>
  <strong>Best response:</strong><br>
  Reduce demands and sensory input. Avoid
  asking multiple questions. Allow me to take
  a break, stim, or have space.
</p>
<p>
  If something is urgent, communicate it
  simply and directly.
</p>
<button
  type="button"
  class="dismiss-button"
  id="dismissAlertButton">
  I'm able to communicate again
</button>
  </div>
</section>
<!-- QUICK COMMUNICATE -->
<section class="section">
  <h2 class="section-title">
    ⚡ Quick Communicate
  </h2>
  <p class="section-description">
    Tap once when finding words is difficult.
  </p>
  <div class="quick-grid">
<button
  type="button"
  class="quick-button"
  data-message="lessTalking">
  <span class="quick-icon">🔇</span>
  Less Talking
</button>
<button
  type="button"
  class="quick-button"
  data-message="break">
  <span class="quick-icon">🧘</span>
  I Need a Break
</button>
<button
  type="button"
  class="quick-button"
  data-message="sensory">
  <span class="quick-icon">🔊</span>
  Too Much Input
</button>
<button
  type="button"
  class="quick-button"
  data-message="demands">
  <span class="quick-icon">🛑</span>
  Reduce Demands
</button>
<button
  type="button"
  class="quick-button"
  data-message="understand">
  <span class="quick-icon">💬</span>
  I Understand
</button>
<button
  type="button"
  class="quick-button"
  data-message="notAngry">
  <span class="quick-icon">❤️</span>
  Not Angry
</button>
<button
  type="button"
  class="quick-button"
  data-message="time">
  <span class="quick-icon">⏳</span>
  Give Me Time
</button>
<button
  type="button"
  class="quick-button"
  data-message="stim">
  <span class="quick-icon">🔄</span>
  I Need to Stim
</button>
  </div>
</section>
<!-- STATUS -->
<section class="section">
  <h2 class="section-title">
    📊 Current System Status
  </h2>
  <p class="section-description">
    Choose the level that best describes your
    current state. The translation updates immediately.
  </p>
  <div id="statusApp"></div>
</section>
<!-- TRANSLATION -->
<section class="section">
  <h2 class="section-title">
    🧠 Translation
  </h2>
  <div id="translationContent"></div>
</section>
<div class="footer">
  Your status is saved on this device.
</div>
</div>
<!-- QUICK MESSAGE OVERLAY -->
<div
  class="message-overlay"
  id="messageOverlay">
  <div
    class="message-icon"
    id="messageIcon"></div>
  <div
    class="message-title"
    id="messageTitle"></div>
  <div
    class="message-text"
    id="messageText"></div>
← Back
  </button>
</div>
<script>
/* =========================================
   QUICK COMMUNICATION
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
    icon: "🔄",
    title: "I NEED TO STIM",
    text:
      "I may need repetitive movement, sounds, fidgeting, pacing, or another form of self-regulation. Please allow this unless there is a genuine safety concern. Stimming may help me regulate and recover capacity."
  }
};
/* =========================================
   STATUS METRICS
========================================= */
const metrics = {
  physical: {
    name: "🫀 Physical Capacity",
    type: "capacity",
    description:
      "How much can my body physically do right now?"
  },
  energy: {
    name: "⚡ Energy",
    type: "capacity",
    description:
      "How much usable energy do I currently have?"
  },
  cognitive: {
    name: "🧠 Cognitive Bandwidth",
    type: "capacity",
    description:
      "How much information and complexity can I process?"
  },
  executive: {
    name: "🎯 Executive Function",
    type: "capacity",
    description:
      "How easily can I start, organize, and switch tasks?"
  },
  communication: {
    name: "💬 Communication Capacity",
    type: "capacity",
    description:
      "How easily can I communicate and respond?"
  },
  social: {
    name: "🤝 Social Capacity",
    type: "capacity",
    description:
      "How much interpersonal interaction can I handle?"
  },
  sensory: {
    name: "🔊 Sensory Load",
    type: "load",
    description:
      "How overloaded am I by sensory input?"
  },
  stress: {
    name: "⚠️ Stress Load",
    type: "load",
    description:
      "How much accumulated pressure am I carrying?"
  },
  demand: {
    name: "📋 Demand Pressure",
    type: "load",
    description:
      "How difficult are requests and expectations right now?"
  },
  transition: {
    name: "🔄 Transition Difficulty",
    type: "load",
    description:
      "How difficult are interruptions or changes right now?"
  }
};
const capacityLabels = [
  "",
  "Critical",
  "Low",
  "Limited",
  "Good",
  "Full"
];
const loadLabels = [
  "",
  "Minimal",
  "Manageable",
  "Elevated",
  "High",
  "Critical"
];
/* =========================================
   SAVED VALUES
========================================= */
const defaultValues = {
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
let values = {
  ...defaultValues,
  ...JSON.parse(
    localStorage.getItem("systemStatus") ||
    "{}"
  )
};
function saveValues() {
  localStorage.setItem(
    "systemStatus",
    JSON.stringify(values)
  );
}
/* =========================================
   RENDER STATUS QUESTIONS
========================================= */
function renderStatus() {
  const app =
    document.getElementById("statusApp");
  app.innerHTML = "";
  renderMetricGroup(
    app,
    "Available Capacity",
    "capacity"
  );
  renderMetricGroup(
    app,
    "Current Load",
    "load"
  );
  updateTranslation();
}
function renderMetricGroup(
  app,
  title,
  type
) {
  const heading =
    document.createElement("div");
  heading.className =
    "status-group-title";
  heading.textContent =
    title;
  app.appendChild(heading);
  Object.entries(metrics)
    .filter(
      ([, metric]) =>
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
    "metric";
  const name =
    document.createElement("div");
  name.className =
    "metric-name";
  name.textContent =
    metric.name;
  const description =
    document.createElement("div");
  description.className =
    "metric-description";
  description.textContent =
    metric.description;
  const levels =
    document.createElement("div");
  levels.className =
    "level-row";
  for (
    let level = 1;
    level <= 5;
    level++
  ) {
    const button =
      document.createElement("button");
    button.type =
      "button";
    button.className =
      "level-button";
    button.textContent =
      level;
    if (
      values[key] === level
    ) {
      button.classList.add(
        "selected"
      );
    }
    button.addEventListener(
      "click",
      function() {
        values[key] =
          level;
        saveValues();
        renderStatus();
      }
    );
    levels.appendChild(
      button
    );
  }
  const label =
    document.createElement("div");
  label.className =
    "level-label";
  const labels =
    metric.type === "capacity"
      ? capacityLabels
      : loadLabels;
  label.textContent =
    labels[
      values[key]
    ];
  card.appendChild(name);
  card.appendChild(description);
  card.appendChild(levels);
  card.appendChild(label);
  return card;
}
/* =========================================
   RESPONSE-FIRST TRANSLATION
========================================= */
function updateTranslation() {
  const capacityKeys =
    Object.keys(metrics)
      .filter(
        key =>
          metrics[key].type ===
          "capacity"
      );
  const loadKeys =
    Object.keys(metrics)
      .filter(
        key =>
          metrics[key].type ===
          "load"
      );
  const capacityAverage =
    capacityKeys.reduce(
      (sum, key) =>
        sum + values[key],
      0
    ) / capacityKeys.length;
  const loadAverage =
    loadKeys.reduce(
      (sum, key) =>
        sum + values[key],
      0
    ) / loadKeys.length;
  /*
    Critical conditions override averages.
    This prevents a serious problem from
    being hidden by otherwise good scores.
  */
  const criticalCapacity =
    capacityKeys.filter(
      key =>
        values[key] === 1
    );
  const highLoad =
    loadKeys.filter(
      key =>
        values[key] >= 5
    );
  const severeIssues =
    criticalCapacity.length +
    highLoad.length;
  let state;
  let response;
  if (
    severeIssues >= 2 ||
    (
      capacityAverage < 2 &&
      loadAverage >= 4
    )
  ) {
    state =
      "🔴 OVERLOADED";
    response =
      "PROTECT AND ALLOW RECOVERY";
  }
  else if (
    severeIssues >= 1 ||
    capacityAverage < 3 ||
    loadAverage >= 3.7
  ) {
    state =
      "🟠 STRAINED";
    response =
      "REDUCE PRESSURE";
  }
  else if (
    capacityAverage < 4 ||
    loadAverage > 2.2
  ) {
    state =
      "🟡 LIMITED";
    response =
      "SIMPLIFY";
  }
  else {
    state =
      "🟢 AVAILABLE";
    response =
      "INTERACT NORMALLY";
  }
  /*
    Rank dominant limiting factors.
  */
  const factors =
    Object.keys(metrics)
      .map(
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
          return {
            key,
            severity
          };
        }
      )
      .sort(
        (a, b) =>
          b.severity -
          a.severity
      );
  const primary =
    factors.slice(0, 3);
  const primaryNames =
    primary
      .map(
        factor =>
          metrics[factor.key].name
      );
  /*
    Build a plain-English explanation.
  */
  const causes = [];
  if (
    values.energy <= 2
  ) {
    causes.push(
      "available energy reserves are low"
    );
  }
  if (
    values.physical <= 2
  ) {
    causes.push(
      "physical capacity is limited"
    );
  }
  if (
    values.cognitive <= 2
  ) {
    causes.push(
      "processing information requires extra effort"
    );
  }
  if (
    values.executive <= 2
  ) {
    causes.push(
      "starting or switching tasks is difficult"
    );
  }
  if (
    values.communication <= 2
  ) {
    causes.push(
      "communicating may be difficult even when understanding is intact"
    );
  }
  if (
    values.social <= 2
  ) {
    causes.push(
      "social interaction is using a large amount of capacity"
    );
  }
  if (
    values.sensory >= 4
  ) {
    causes.push(
      "sensory input is consuming significant capacity"
    );
  }
  if (
    values.stress >= 4
  ) {
    causes.push(
      "accumulated stress is increasing the cost of ordinary tasks"
    );
  }
  if (
    values.demand >= 4
  ) {
    causes.push(
      "current expectations and demands are creating additional pressure"
    );
  }
  if (
    values.transition >= 4
  ) {
    causes.push(
      "interruptions and changes require extra effort"
    );
  }
  let happening;
  if (
    causes.length === 0
  ) {
    happening =
      "Current capacity appears generally available for normal activity.";
  }
  else if (
    causes.length === 1
  ) {
    happening =
      "The main limiting factor is that " +
      causes[0] +
      ".";
  }
  else {
    happening =
      "Current capacity is being affected because " +
      causes.slice(0, 2).join(" and ") +
      ".";
  }
  /*
    Observable behavior.
  */
  const notice = [];
  if (
    values.sensory >= 4
  ) {
    notice.push(
      "Increased stimming or attempts to self-regulate."
    );
    notice.push(
      "A need for quiet, reduced stimulation, or a break."
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
    values.stress >= 4
  ) {
    notice.push(
      "Reduced patience or a stronger need for space."
    );
  }
  if (
    notice.length === 0
  ) {
    notice.push(
      "No major outward signs of reduced capacity may be obvious."
    );
  }
  /*
    Helpful responses.
  */
  const actions = [];
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
      "Keep communication clear and direct."
    );
    actions.push(
      "Avoid unnecessary complexity or stacking multiple requests."
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
      "A break may help preserve or restore capacity."
    );
    actions.push(
      "Give one thing at a time when possible."
    );
  }
  if (
    response ===
    "PROTECT AND ALLOW RECOVERY"
  ) {
    actions.push(
      "Reduce demands and sensory input as soon as possible."
    );
    actions.push(
      "Do not require an explanation or extended conversation."
    );
    actions.push(
      "Allow space, a break, withdrawal, or stimming for self-regulation."
    );
  }
  /*
    Add specific recommendations.
  */
  if (
    values.sensory >= 4
  ) {
    actions.push(
      "Reduce noise, interruptions, and other unnecessary sensory input."
    );
  }
  if (
    values.communication <= 2
  ) {
    actions.push(
      "Do not assume reduced communication means lack of understanding."
    );
  }
  if (
    values.transition >= 4
  ) {
    actions.push(
      "Give advance warning before changes when possible."
    );
  }
  /*
    Render translation.
  */
  const translation =
    document.getElementById(
      "translationContent"
    );
  translation.innerHTML = `
    <div class="translation-state">
      ${state}
    </div>
    <div class="response-box">
      <span class="response-label">
        BEST RESPONSE
      </span>
      ${response}
    </div>
    <div class="translation-block">
      <h3>
        What is happening
      </h3>
      <p>
        ${happening}
      </p>
    </div>
    <div class="translation-block">
      <h3>
        What you may notice
      </h3>
      <ul>
        ${notice
          .map(
            item =>
              `<li>${item}</li>`
          )
          .join("")}
      </ul>
    </div>
    <div class="translation-block">
      <h3>
        What helps
      </h3>
      <ul>
        ${actions
          .map(
            item =>
              `<li>${item}</li>`
          )
          .join("")}
      </ul>
    </div>
    <div class="translation-block">
      <h3>
        Primary factors
      </h3>
      <p>
        ${primaryNames.join(" • ")}
      </p>
    </div>
  `;
}
/* =========================================
   BUTTON EVENT LISTENERS
========================================= */
/* Red Alert */
document
  .getElementById(
    "redAlertButton"
  )
  .addEventListener(
    "click",
    function() {
      document
        .getElementById(
          "alertPanel"
        )
        .classList.add(
          "active"
        );
    }
  );
document
  .getElementById(
    "dismissAlertButton"
  )
  .addEventListener(
    "click",
    function() {
      document
        .getElementById(
          "alertPanel"
        )
        .classList.remove(
          "active"
        );
    }
  );
/* Quick Communication */
document
  .querySelectorAll(
    ".quick-button"
  )
  .forEach(
    button => {
      button.addEventListener(
        "click",
        function() {
          const key =
            button.dataset.message;
          const message =
            messages[key];
          document
            .getElementById(
              "messageIcon"
            )
            .textContent =
              message.icon;
          document
            .getElementById(
              "messageTitle"
            )
            .textContent =
              message.title;
          document
            .getElementById(
              "messageText"
            )
            .textContent =
              message.text;
          document
            .getElementById(
              "messageOverlay"
            )
            .classList.add(
              "active"
            );
        }
      );
    }
  );
document
  .getElementById(
    "messageBackButton"
  )
  .addEventListener(
    "click",
    function() {
      document
        .getElementById(
          "messageOverlay"
        )
        .classList.remove(
          "active"
        );
    }
  );
/* =========================================
   START APP
========================================= */
renderStatus();
</script>
</body>
</html>
