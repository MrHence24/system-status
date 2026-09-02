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
  --bg: #111;
  --card: #1d1d1f;
  --text: #ffffff;
  --muted: #a1a1a6;
}
* {
  box-sizing: border-box;
}
body {
  margin: 0;
  padding: 20px;
  background: var(--bg);
  color: var(--text);
  font-family: -apple-system, BlinkMacSystemFont, sans-serif;
}
h1 {
  text-align: center;
  margin: 10px 0 5px;
}
.subtitle {
  text-align: center;
  color: var(--muted);
  margin-bottom: 20px;
}
/* RED ALERT */
#red-alert-button {
  width: 100%;
  padding: 18px;
  border: none;
  border-radius: 18px;
  font-size: 20px;
  font-weight: 800;
  background: #ff453a;
  color: white;
  margin-bottom: 20px;
}
#red-alert-button:active {
  transform: scale(.97);
}
.red-alert-active {
  background: #2b1111 !important;
  border: 2px solid #ff453a !important;
}
.red-alert-banner {
  background: #ff453a;
  border-radius: 18px;
  padding: 18px;
  margin-bottom: 20px;
  font-weight: 600;
  line-height: 1.45;
}
.dismiss-alert {
  width: 100%;
  margin-top: 12px;
  padding: 12px;
  border: none;
  border-radius: 10px;
  font-size: 16px;
}
/* SECTIONS */
.section-title {
  font-size: 13px;
  color: var(--muted);
  text-transform: uppercase;
  letter-spacing: 1px;
  margin: 28px 5px 10px;
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
  margin-bottom: 4px;
}
.status-description {
  font-size: 13px;
  color: var(--muted);
  margin-bottom: 14px;
}
.levels {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 7px;
}
.level {
  border: 1px solid #444;
  background: #2a2a2c;
  color: white;
  border-radius: 10px;
  padding: 11px 2px;
  font-size: 17px;
  font-weight: bold;
}
.level.selected {
  background: white;
  color: black;
  border-color: white;
}
.level-label {
  display: block;
  font-size: 8px;
  margin-top: 4px;
  font-weight: normal;
}
/* SUMMARY */
#summary {
  background: #222;
  border-radius: 20px;
  padding: 20px;
  margin-top: 30px;
  margin-bottom: 25px;
}
#summary h2 {
  margin-top: 0;
}
.system-state {
  font-size: 21px;
  font-weight: bold;
  margin-bottom: 12px;
}
.bottleneck {
  background: #2d2d30;
  border-radius: 12px;
  padding: 12px;
  margin-top: 10px;
}
.pattern {
  margin-top: 16px;
  padding: 14px;
  border-radius: 12px;
  background: #292929;
}
.summary-text {
  line-height: 1.5;
  color: #ddd;
  margin-top: 14px;
}
.summary-section {
  margin-top: 20px;
}
.summary-section h3 {
  font-size: 16px;
}
.summary-section ul {
  padding-left: 20px;
  line-height: 1.5;
  color: #ccc;
}
.reset {
  width: 100%;
  padding: 14px;
  border-radius: 14px;
  border: none;
  font-size: 16px;
  margin-bottom: 30px;
}
.hidden {
  display: none;
}
</style>
</head>
<body>
<h1>🧠 System Status</h1>
<div class="subtitle">
  How is the system operating right now?
</div>
<button id="red-alert-button" onclick="activateRedAlert()">
  🚨 RED ALERT — TOO OVERLOADED TO ASSESS
</button>
<div id="red-alert-area"></div>
<div id="normal-app">
  <div id="app"></div>
  <div id="summary">
<h2>Translation</h2>
<div id="summary-content"></div>
  </div>
  <button class="reset" onclick="resetAll()">
    Reset to baseline
  </button>
</div>
<script>
const metrics = {
  physical: {
    name: "🫀 Physical Capacity",
    short: "Physical Capacity",
    type: "capacity",
    description: "How much can my body physically do right now?"
  },
  energy: {
    name: "⚡ Energy",
    short: "Energy",
    type: "capacity",
    description: "How much usable energy do I have?"
  },
  cognitive: {
    name: "🧠 Cognitive Bandwidth",
    short: "Cognitive Bandwidth",
    type: "capacity",
    description: "How much information and complexity can I process?"
  },
  executive: {
    name: "🎯 Executive Function",
    short: "Executive Function",
    type: "capacity",
    description: "How easily can I start, organize, and complete tasks?"
  },
  communication: {
    name: "💬 Communication Capacity",
    short: "Communication Capacity",
    type: "capacity",
    description: "How much communication can I produce and process?"
  },
  social: {
    name: "🤝 Social Capacity",
    short: "Social Capacity",
    type: "capacity",
    description: "How much interpersonal interaction can I handle?"
  },
  sensory: {
    name: "🔊 Sensory Load",
    short: "Sensory Load",
    type: "load",
    description: "How overloaded am I by sensory input?"
  },
  stress: {
    name: "⚠️ Stress Load",
    short: "Stress Load",
    type: "load",
    description: "How much accumulated pressure is my system carrying?"
  },
  demand: {
    name: "📋 Demand Pressure",
    short: "Demand Pressure",
    type: "load",
    description: "How strongly is my system resisting expectations and demands?"
  },
  transition: {
    name: "🔄 Transition Difficulty",
    short: "Transition Difficulty",
    type: "load",
    description: "How difficult is it to switch tasks or change plans?"
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
let values = JSON.parse(localStorage.getItem("systemStatus")) || {
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
let redAlert =
  JSON.parse(localStorage.getItem("redAlert")) || false;
/* -------------------- */
/* RED ALERT */
/* -------------------- */
function activateRedAlert() {
  redAlert = true;
  localStorage.setItem(
    "redAlert",
    JSON.stringify(true)
  );
  renderApp();
}
function dismissRedAlert() {
  redAlert = false;
  localStorage.setItem(
    "redAlert",
    JSON.stringify(false)
  );
  renderApp();
}
/* -------------------- */
/* RENDER */
/* -------------------- */
function renderApp() {
  const normalApp =
    document.getElementById("normal-app");
  const alertArea =
    document.getElementById("red-alert-area");
  if (redAlert) {
    normalApp.classList.add("hidden");
    alertArea.innerHTML = `
      <div class="red-alert-banner">
        <h2>🚨 SYSTEM OVERLOADED</h2>
        I am currently too overloaded to accurately
        explain or assess what is happening.
        <br><br>
        Please do not interpret reduced communication,
        delayed responses, silence, or difficulty answering
        questions as anger, disrespect, or lack of care.
        <br><br>
        The most helpful response right now is to reduce
        demands, avoid asking multiple questions, minimize
        sensory input, and allow time and space for recovery.
        <br><br>
        If something is urgent, communicate it clearly,
        directly, and simply.
        <button class="dismiss-alert"
          onclick="dismissRedAlert()">
          I'm able to assess again
        </button>
      </div>
    `;
    return;
  }
  normalApp.classList.remove("hidden");
  alertArea.innerHTML = "";
  const app =
    document.getElementById("app");
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
  updateSummary();
}
function addSection(
  app,
  title,
  type
) {
  const sectionTitle =
    document.createElement("div");
  sectionTitle.className =
    "section-title";
  sectionTitle.textContent =
    title;
  app.appendChild(sectionTitle);
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
  const name =
    document.createElement("div");
  name.className =
    "status-name";
  name.textContent =
    metric.name;
  const description =
    document.createElement("div");
  description.className =
    "status-description";
  description.textContent =
    metric.description;
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
      '<span class="level-label">' +
      labels[level] +
      '</span>';
    button.onclick = () => {
      values[key] =
        level;
      save();
      renderApp();
    };
    levels.appendChild(
      button
    );
  }
  card.appendChild(
    name
  );
  card.appendChild(
    description
  );
  card.appendChild(
    levels
  );
  return card;
}
function save() {
  localStorage.setItem(
    "systemStatus",
    JSON.stringify(values)
  );
}
/* -------------------- */
/* BOTTLENECK ENGINE */
/* -------------------- */
function getBottlenecks() {
  let limitations = [];
  Object.keys(metrics)
    .forEach(key => {
      const metric =
        metrics[key];
      let severity;
      if (
        metric.type ===
        "capacity"
      ) {
        severity =
          6 - values[key];
      }
      else {
        severity =
          values[key];
      }
      limitations.push({
        key,
        name:
          metric.short,
        severity
      });
    });
  limitations.sort(
    (
      a,
      b
    ) =>
      b.severity -
      a.severity
  );
  return {
    primary:
      limitations[0],
    secondary:
      limitations[1]
  };
}
/* -------------------- */
/* PATTERN ENGINE */
/* -------------------- */
function detectPattern() {
  /* FUEL WITHOUT TRACTION */
  if (
    values.energy >= 4 &&
    values.executive <= 2
  ) {
    return {
      name:
        "⚡ Fuel Without Traction",
      description:
        "Energy is available, but converting intention into action is currently difficult. From the outside, this may look like having enough energy but still struggling to begin or organize tasks."
    };
  }
  /* CAPABLE BUT OVERLOADED */
  if (
    values.cognitive >= 4 &&
    values.sensory >= 4
  ) {
    return {
      name:
        "🧠 Capable but Overloaded",
      description:
        "Thinking capacity is largely intact, but environmental input is consuming a disproportionate amount of available resources. Reducing sensory input may restore function more effectively than pushing harder."
    };
  }
  /* EVERYTHING IS FRICTION */
  if (
    values.executive <= 3 &&
    values.demand >= 4 &&
    values.transition >= 4
  ) {
    return {
      name:
        "🧱 Everything Is Friction",
      description:
        "Starting, switching, and responding to expectations are all carrying additional resistance. Individual tasks may be possible, but the accumulated friction makes ordinary activities significantly more costly."
    };
  }
  /* PUSHING THROUGH */
  if (
    values.stress >= 4 &&
    values.demand >= 4 &&
    values.energy >= 2
  ) {
    return {
      name:
        "🔥 Pushing Through",
      description:
        "The system may still be completing tasks, but it is doing so under sustained pressure rather than from comfortable reserves. Continued demands may cause a sharper reduction in capacity later."
    };
  }
  /* SOCIAL DEPLETION */
  if (
    values.social <= 2 &&
    values.communication <= 2
  ) {
    return {
      name:
        "🤝 Socially Depleted",
      description:
        "Interpersonal interaction and communication are currently expensive. Reduced engagement should not automatically be interpreted as rejection, anger, or lack of desire for connection."
    };
  }
  /* ENERGY DEPLETION */
  if (
    values.energy <= 2 &&
    values.physical <= 2
  ) {
    return {
      name:
        "🔋 Resource Depletion",
      description:
        "The primary limitation appears to be depleted physical and general energy reserves. Restoring resources may be more useful right now than increasing structure or motivation."
    };
  }
  /* HIGH PRESSURE */
  if (
    values.stress >= 4 &&
    values.demand >= 4
  ) {
    return {
      name:
        "⚠️ High-Pressure State",
      description:
        "Background stress and current expectations are both placing substantial pressure on the system. Even relatively small additional demands may have a larger-than-expected impact."
    };
  }
  return {
    name:
      "⚙️ Mixed System State",
    description:
      "No single dominant pattern is currently standing out. Capacity and load are interacting across multiple areas."
  };
}
/* -------------------- */
/* TRANSLATION ENGINE */
/* -------------------- */
function updateSummary() {
  const bottlenecks =
    getBottlenecks();
  const pattern =
    detectPattern();
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
  const averageCapacity =
    capacityKeys.reduce(
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
  const averageLoad =
    loadKeys.reduce(
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
  if (
    averageCapacity >= 4 &&
    averageLoad <= 2
  ) {
    state =
      "🟢 Good Capacity";
  }
  else if (
    averageCapacity >= 3.5 &&
    averageLoad <= 3
  ) {
    state =
      "🟡 Functional";
  }
  else if (
    averageCapacity >= 2.5
  ) {
    state =
      "🟠 Strained";
  }
  else {
    state =
      "🔴 Low Capacity";
  }
  const effects = [];
  if (
    values.executive <= 2
  ) {
    effects.push(
      "Understanding what needs to happen does not necessarily mean starting or organizing it is currently easy."
    );
  }
  if (
    values.communication <= 2
  ) {
    effects.push(
      "Communication may be reduced even when attention, care, or understanding are still present."
    );
  }
  if (
    values.cognitive <= 2
  ) {
    effects.push(
      "Complex information, multiple choices, and lengthy explanations may be difficult to process right now."
    );
  }
  if (
    values.sensory >= 4
  ) {
    effects.push(
      "Environmental input may be consuming resources that would otherwise be available for thinking, communication, or tasks."
    );
  }
  if (
    values.transition >= 4
  ) {
    effects.push(
      "Changing activities or adapting to interruptions may require substantially more effort than usual."
    );
  }
  if (
    values.demand >= 4
  ) {
    effects.push(
      "Requests and expectations may create resistance disproportionate to the actual size of the task."
    );
  }
  if (
    values.energy <= 2
  ) {
    effects.push(
      "Available reserves are limited, so even manageable activities may have a significant recovery cost."
    );
  }
  if (
    effects.length === 0
  ) {
    effects.push(
      "No major individual limitation is currently standing out."
    );
  }
  const support = [];
  if (
    values.executive <= 2
  ) {
    support.push(
      "Provide a concrete first step rather than a broad instruction."
    );
  }
  if (
    values.cognitive <= 2
  ) {
    support.push(
      "Give information in smaller pieces and reduce unnecessary decisions."
    );
  }
  if (
    values.sensory >= 4
  ) {
    support.push(
      "Reduce noise, interruptions, and competing sensory input where possible."
    );
  }
  if (
    values.demand >= 4
  ) {
    support.push(
      "Use collaborative and low-pressure language when possible."
    );
  }
  if (
    values.transition >= 4
  ) {
    support.push(
      "Give advance notice before transitions or changes whenever possible."
    );
  }
  if (
    values.energy <= 2
  ) {
    support.push(
      "Prioritize essential activities and protect time for recovery."
    );
  }
  if (
    support.length === 0
  ) {
    support.push(
      "Normal expectations and interaction are likely manageable."
    );
  }
  document
    .getElementById(
      "summary-content"
    )
    .innerHTML = `
      <div class="system-state">
        ${state}
      </div>
      <div class="bottleneck">
        <strong>
          🎯 Primary Bottleneck
        </strong>
        <br>
        ${bottlenecks.primary.name}
      </div>
      <div class="bottleneck">
        <strong>
          🥈 Secondary Bottleneck
        </strong>
        <br>
        ${bottlenecks.secondary.name}
      </div>
      <div class="pattern">
        <strong>
          ${pattern.name}
        </strong>
        <br><br>
        ${pattern.description}
      </div>
      <div class="summary-section">
        <h3>
          What this may look like
        </h3>
        <ul>
          ${effects
            .map(
              item =>
                `<li>${item}</li>`
            )
            .join("")
          }
        </ul>
      </div>
      <div class="summary-section">
        <h3>
          What helps right now
        </h3>
        <ul>
          ${support
            .map(
              item =>
                `<li>${item}</li>`
            )
            .join("")
          }
        </ul>
      </div>
    `;
}
/* -------------------- */
/* RESET */
/* -------------------- */
function resetAll() {
  Object.keys(values)
    .forEach(
      key => {
        values[key] = 3;
      }
    );
  save();
  renderApp();
}
renderApp();
</script>
</body>
</html>
