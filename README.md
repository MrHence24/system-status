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
  padding: 16px;
  background: var(--bg);
  color: var(--text);
  font-family: -apple-system, BlinkMacSystemFont, sans-serif;
}
h1 {
  text-align: center;
  margin: 8px 0 4px;
  font-size: 28px;
}
.subtitle {
  text-align: center;
  color: var(--muted);
  font-size: 14px;
  margin-bottom: 20px;
}
/* RED ALERT */
.alert-button {
  width: 100%;
  background: var(--red);
  border: none;
  color: white;
  border-radius: 20px;
  padding: 20px;
  font-size: 20px;
  font-weight: 900;
  margin-bottom: 16px;
}
.alert-box {
  background: #321616;
  border: 2px solid var(--red);
  border-radius: 20px;
  padding: 20px;
  margin-bottom: 20px;
  line-height: 1.5;
}
.dismiss {
  width: 100%;
  padding: 14px;
  border-radius: 14px;
  border: none;
  margin-top: 12px;
  font-size: 16px;
}
/* SECTION */
.section-title {
  font-size: 13px;
  text-transform: uppercase;
  letter-spacing: 1px;
  color: var(--muted);
  margin: 28px 5px 12px;
}
/* QUICK COMMUNICATION */
.quick-intro {
  color: var(--muted);
  margin-bottom: 14px;
  line-height: 1.4;
}
.quick-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 10px;
}
.quick-button {
  min-height: 110px;
  border: none;
  border-radius: 20px;
  padding: 12px 8px;
  color: white;
  background: var(--card);
  font-size: 16px;
  font-weight: 700;
}
.quick-button:active {
  transform: scale(.97);
}
.quick-icon {
  display: block;
  font-size: 32px;
  margin-bottom: 7px;
}
/* STATUS QUESTIONS */
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
  font-size: 16px;
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
/* TRANSLATION */
#translation {
  background: var(--card);
  border-radius: 20px;
  padding: 20px;
  margin-top: 25px;
  margin-bottom: 30px;
}
.system-state {
  font-size: 25px;
  font-weight: 800;
  margin-bottom: 10px;
}
.best-response {
  background: var(--card2);
  padding: 16px;
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
/* FULL SCREEN MESSAGE */
#message-overlay {
  display: none;
  position: fixed;
  inset: 0;
  background: var(--bg);
  z-index: 100;
  padding: 25px;
}
#message-overlay.active {
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
}
.message-icon {
  font-size: 70px;
}
.message-title {
  font-size: 30px;
  font-weight: 800;
  margin: 20px 0;
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
</style>
</head>
<body>
<h1>🧠 System Status</h1>
<div class="subtitle">
  Real-time accessibility & communication
</div>
<!-- RED ALERT -->

🚨 RED ALERT — TOO OVERLOADED TO EXPLAIN

</button>
<div id="alert-content"></div>
<!-- QUICK COMMUNICATION -->
<div class="section-title">
  ⚡ Quick Communicate
</div>
<div class="quick-intro">
  Tap once when finding words is difficult.
</div>
<div class="quick-grid">

🔇
Less Talking
🧘
I Need a Break
🔊
Too Much Input
🛑
Reduce Demands
💬
I Understand
❤️
Not Angry
⏳
Give Me Time
🧠
I Need to Stim
</div>
<!-- STATUS -->
<div class="section-title">
  📊 Current System Status
</div>
<div id="status-app"></div>
<!-- TRANSLATION -->
<div id="translation">
  <h2>Translation</h2>
  <div id="translation-content"></div>
</div>
<!-- FULL SCREEN MESSAGE -->
<div id="message-overlay">
  <div class="message-icon"
    id="message-icon"></div>
  <div class="message-title"
    id="message-title"></div>
  <div class="message-text"
    id="message-text"></div>
← Back
  </button>
</div>
<script>
/* QUICK MESSAGES */
const messages = {
  lessTalking: {
    icon: "🔇",
    title: "I NEED LESS TALKING",
    text: "I am having difficulty processing and responding to conversation right now. Please reduce unnecessary questions and give me time to process. I may understand what you are saying even if I cannot respond normally."
  },
  break: {
    icon: "🧘",
    title: "I NEED A BREAK",
    text: "My current capacity is reduced and I need time away from demands or stimulation. Please allow me to take a break without requiring me to explain or justify it."
  },
  sensory: {
    icon: "🔊",
    title: "TOO MUCH INPUT",
    text: "My nervous system is receiving more sensory input than I can comfortably process right now. Reducing noise, talking, interruptions, light, touch, or other stimulation would help."
  },
  demands: {
    icon: "🛑",
    title: "PLEASE REDUCE DEMANDS",
    text: "Additional requests or expectations are difficult for me to process right now. Please avoid adding unnecessary demands and focus on what is actually urgent."
  },
  understand: {
    icon: "💬",
    title: "I UNDERSTAND",
    text: "I may understand what you are saying even though I am having difficulty responding. Please do not assume silence or delayed communication means I am ignoring you."
  },
  notAngry: {
    icon: "❤️",
    title: "I'M NOT ANGRY",
    text: "My reduced communication, facial expression, withdrawal, or need for space does not necessarily mean I am angry or upset with you. I currently have limited capacity to interact."
  },
  time: {
    icon: "⏳",
    title: "PLEASE GIVE ME TIME",
    text: "I need additional time to process what is happening and determine how to respond. Please avoid repeatedly asking for an immediate answer."
  },
  stim: {
    icon: "🧠",
    title: "I NEED TO STIM",
    text: "I may need repetitive movement, sounds, fidgeting, pacing, or another form of self-regulation. Please allow this unless there is a genuine safety concern. Stimming may help me regulate and recover capacity."
  }
};
function showMessage(key) {
  const message = messages[key];
  document.getElementById("message-icon").textContent =
    message.icon;
  document.getElementById("message-title").textContent =
    message.title;
  document.getElementById("message-text").textContent =
    message.text;
  document
    .getElementById("message-overlay")
    .classList.add("active");
}
function closeMessage() {
  document
    .getElementById("message-overlay")
    .classList.remove("active");
}
/* RED ALERT */
function activateAlert() {
  document
    .getElementById("alert-content")
    .innerHTML = `
      <div class="alert-box">
        <h2>🚨 SYSTEM OVERLOADED</h2>
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
          <strong>BEST RESPONSE:</strong><br>
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
/* STATUS DATA */
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
/* RENDER QUESTIONS */
function renderStatus() {
  const app =
    document.getElementById("status-app");
  app.innerHTML = "";
  addSection(
    app,
    "Available Capacity",
    "capacity"
  );
  addSection(
    app,
    "Current Load",
    "load"
  );
  updateTranslation();
}
function addSection(
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
  app.appendChild(heading);
  Object.entries(metrics)
    .filter(
      ([key, metric]) =>
        metric.type === type
    )
    .forEach(
      ([key, metric]) =>
        app.appendChild(
          createMetric(
            key,
            metric
          )
        )
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
    button.innerHTML = `
      ${level}
      <span class="level-label">
        ${labels[level]}
      </span>
    `;
    button.onclick =
      () => {
        values[key] = level;
        localStorage.setItem(
          "systemStatus",
          JSON.stringify(values)
        );
        renderStatus();
      };
    levels.appendChild(button);
  }
  card.appendChild(levels);
  return card;
}
/* RESPONSE-FIRST TRANSLATOR */
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
  const avgCapacity =
    capacityKeys.reduce(
      (sum, key) =>
        sum + values[key],
      0
    ) / capacityKeys.length;
  const avgLoad =
    loadKeys.reduce(
      (sum, key) =>
        sum + values[key],
      0
    ) / loadKeys.length;
  let state;
  let response;
  if (
    avgCapacity >= 4 &&
    avgLoad <= 2
  ) {
    state = "🟢 AVAILABLE";
    response = "INTERACT NORMALLY";
  }
  else if (
    avgCapacity >= 3 &&
    avgLoad <= 3
  ) {
    state = "🟡 LIMITED";
    response = "SIMPLIFY";
  }
  else if (
    avgCapacity >= 2.3
  ) {
    state = "🟠 STRAINED";
    response = "REDUCE PRESSURE";
  }
  else {
    state = "🔴 OVERLOADED";
    response = "PROTECT AND ALLOW RECOVERY";
  }
  const issues = [];
  Object.keys(metrics)
    .forEach(key => {
      const severity =
        metrics[key].type === "capacity"
          ? 6 - values[key]
          : values[key];
      issues.push({
        key,
        severity
      });
    });
  issues.sort(
    (a, b) =>
      b.severity - a.severity
  );
  const primary =
    issues.slice(0, 3);
  const factorNames =
    primary
      .map(
        item =>
          metrics[item.key].name
      )
      .join(" • ");
  let notice = [];
  let actions = [];
  if (values.sensory >= 4) {
    notice.push(
      "Increased stimming or attempts to regulate sensory input."
    );
    notice.push(
      "A need for quiet, space, or a break."
    );
    actions.push(
      "Reduce unnecessary noise and sensory input."
    );
  }
  if (values.communication <= 2) {
    notice.push(
      "Short, delayed, or absent responses."
    );
    actions.push(
      "Do not assume reduced communication means lack of understanding."
    );
  }
  if (values.executive <= 2) {
    notice.push(
      "Difficulty starting or switching tasks."
    );
    actions.push(
      "Give one concrete step at a time."
    );
  }
  if (values.demand >= 4) {
    actions.push(
      "Reduce unnecessary requests and expectations."
    );
  }
  if (values.transition >= 4) {
    notice.push(
      "Difficulty with interruptions or sudden changes."
    );
    actions.push(
      "Give advance warning before transitions when possible."
    );
  }
  if (values.social <= 2) {
    notice.push(
      "Withdrawal or reduced interaction."
    );
    actions.push(
      "Allow space without assuming rejection."
    );
  }
  if (notice.length === 0) {
    notice.push(
      "No major outward signs of reduced capacity may be obvious."
    );
  }
  if (response === "INTERACT NORMALLY") {
    actions.unshift(
      "Normal conversation and expectations are generally manageable."
    );
  }
  if (response === "SIMPLIFY") {
    actions.unshift(
      "Keep communication clear and avoid unnecessary complexity."
    );
  }
  if (response === "REDUCE PRESSURE") {
    actions.unshift(
      "Reduce unnecessary questions, decisions, and demands."
    );
    actions.unshift(
      "A break may help restore capacity."
    );
  }
  if (response === "PROTECT AND ALLOW RECOVERY") {
    actions.unshift(
      "Reduce demands and sensory input immediately where possible."
    );
    actions.unshift(
      "Do not require conversation or an explanation."
    );
    actions.unshift(
      "Allow a break, space, and self-regulation such as stimming."
    );
  }
  document
    .getElementById(
      "translation-content"
    )
    .innerHTML = `
      <div class="system-state">
        ${state}
      </div>
      <div class="best-response">
        BEST RESPONSE:<br>
        ${response}
      </div>
      <div class="translation-section">
        <h3>What is happening</h3>
        <p>
          Current limitations are primarily related to
          ${factorNames}.
        </p>
      </div>
      <div class="translation-section">
        <h3>What you may notice</h3>
        <ul>
          ${notice.map(
            item => `<li>${item}</li>`
          ).join("")}
        </ul>
      </div>
      <div class="translation-section">
        <h3>What helps</h3>
        <ul>
          ${actions.map(
            item => `<li>${item}</li>`
          ).join("")}
        </ul>
      </div>
    `;
}
renderStatus();
</script>
</body>
</html>
