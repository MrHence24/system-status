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
  --text: #fff;
  --muted: #aaa;
  --selected: #ffffff;
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
  margin-bottom: 25px;
}

.section-title {
  font-size: 14px;
  color: #aaa;
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
  font-weight: 600;
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
  padding: 12px 3px;
  font-size: 18px;
  font-weight: bold;
}

.level.selected {
  background: white;
  color: black;
  border-color: white;
}

.level-label {
  display: block;
  font-size: 9px;
  margin-top: 4px;
  font-weight: normal;
}

#summary {
  background: #222;
  border-radius: 20px;
  padding: 20px;
  margin-top: 30px;
  margin-bottom: 30px;
}

#summary h2 {
  margin-top: 0;
}

.summary-state {
  font-size: 22px;
  font-weight: bold;
  margin-bottom: 15px;
}

.summary-text {
  line-height: 1.5;
  color: #ddd;
}

.summary-section {
  margin-top: 18px;
}

.summary-section h3 {
  font-size: 16px;
  margin-bottom: 8px;
}

.summary-section ul {
  padding-left: 20px;
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
</style>
</head>

<body>

<h1>🧠 System Status</h1>
<div class="subtitle">How is the system operating right now?</div>

<div id="app"></div>

<div id="summary">
  <h2>Translation</h2>
  <div id="summary-content"></div>
</div>

<button class="reset" onclick="resetAll()">Reset to baseline</button>

<script>

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
    description: "How strongly is my system resisting expectations and demands?"
  },

  transition: {
    name: "🔄 Transition Difficulty",
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

function renderApp() {

  const app = document.getElementById("app");

  app.innerHTML = "";

  const capacityTitle = document.createElement("div");
  capacityTitle.className = "section-title";
  capacityTitle.textContent = "Available Capacity";

  app.appendChild(capacityTitle);

  Object.entries(metrics)
    .filter(([key, metric]) => metric.type === "capacity")
    .forEach(([key, metric]) => {
      app.appendChild(createMetric(key, metric));
    });

  const loadTitle = document.createElement("div");
  loadTitle.className = "section-title";
  loadTitle.textContent = "Current Load";

  app.appendChild(loadTitle);

  Object.entries(metrics)
    .filter(([key, metric]) => metric.type === "load")
    .forEach(([key, metric]) => {
      app.appendChild(createMetric(key, metric));
    });

  updateSummary();
}

function createMetric(key, metric) {

  const card = document.createElement("div");
  card.className = "status";

  const name = document.createElement("div");
  name.className = "status-name";
  name.textContent = metric.name;

  const description = document.createElement("div");
  description.className = "status-description";
  description.textContent = metric.description;

  const levels = document.createElement("div");
  levels.className = "levels";

  for (let level = 1; level <= 5; level++) {

    const button = document.createElement("button");

    button.className = "level";

    if (values[key] === level) {
      button.classList.add("selected");
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
      values[key] = level;
      localStorage.setItem(
        "systemStatus",
        JSON.stringify(values)
      );
      renderApp();
    };

    levels.appendChild(button);
  }

  card.appendChild(name);
  card.appendChild(description);
  card.appendChild(levels);

  return card;
}

function updateSummary() {

  const capacityKeys = Object.keys(metrics)
    .filter(key => metrics[key].type === "capacity");

  const loadKeys = Object.keys(metrics)
    .filter(key => metrics[key].type === "load");

  const averageCapacity =
    capacityKeys.reduce((sum, key) => sum + values[key], 0) /
    capacityKeys.length;

  const averageLoad =
    loadKeys.reduce((sum, key) => sum + values[key], 0) /
    loadKeys.length;

  let state;
  let explanation;

  if (
    averageCapacity >= 4 &&
    averageLoad <= 2
  ) {

    state = "🟢 System State: Good Capacity";

    explanation =
      "The system currently has substantial available capacity and relatively manageable load. Normal activities and interaction are likely sustainable.";

  }

  else if (
    averageCapacity >= 3 &&
    averageLoad <= 3
  ) {

    state = "🟡 System State: Functional but Limited";

    explanation =
      "The system is functional, but available resources are limited. Normal activities are possible, although additional demands may have a noticeable cost.";

  }

  else if (
    averageCapacity >= 2.5
  ) {

    state = "🟠 System State: Strained";

    explanation =
      "The system is operating under significant pressure. Necessary tasks may still be possible, but additional demands, sensory input, or complex decisions may quickly reduce capacity.";

  }

  else {

    state = "🔴 System State: Low Capacity";

    explanation =
      "Available resources are significantly reduced. The priority should be preserving capacity, reducing unnecessary demands, and allowing recovery.";

  }

  let expectations = [];

  if (values.executive <= 2) {
    expectations.push(
      "Knowing what needs to be done does not necessarily mean task initiation or organization is currently easy."
    );
  }

  if (values.communication <= 2) {
    expectations.push(
      "Reduced communication should not automatically be interpreted as anger, avoidance, or lack of care."
    );
  }

  if (values.social <= 2) {
    expectations.push(
      "Interpersonal interaction may be costly even if connection is still wanted."
    );
  }

  if (values.sensory >= 4) {
    expectations.push(
      "Noise, activity, touch, or multiple simultaneous inputs may have a disproportionately strong impact right now."
    );
  }

  if (values.demand >= 4) {
    expectations.push(
      "Additional requests or pressure may create more difficulty than the objective size of the task would suggest."
    );
  }

  if (values.transition >= 4) {
    expectations.push(
      "Interruptions, sudden changes, and switching tasks may be especially difficult right now."
    );
  }

  if (expectations.length === 0) {
    expectations.push(
      "No major functional limitations are currently standing out."
    );
  }

  let support = [];

  if (averageLoad >= 3) {
    support.push(
      "Reduce unnecessary demands and environmental stimulation."
    );
  }

  if (values.cognitive <= 3) {
    support.push(
      "Communicate important information clearly and avoid presenting too many decisions at once."
    );
  }

  if (values.executive <= 3) {
    support.push(
      "Specific, concrete requests are easier to process than broad or open-ended expectations."
    );
  }

  if (values.energy <= 2) {
    support.push(
      "Prioritize essential activities and allow recovery before adding additional commitments."
    );
  }

  if (support.length === 0) {
    support.push(
      "Normal interaction and expectations are likely manageable."
    );
  }

  document.getElementById("summary-content").innerHTML = `

    <div class="summary-state">
      ${state}
    </div>

    <div class="summary-text">
      ${explanation}
    </div>

    <div class="summary-section">
      <h3>What others may notice</h3>
      <ul>
        ${expectations.map(item => `<li>${item}</li>`).join("")}
      </ul>
    </div>

    <div class="summary-section">
      <h3>What helps right now</h3>
      <ul>
        ${support.map(item => `<li>${item}</li>`).join("")}
      </ul>
    </div>

  `;
}

function resetAll() {

  Object.keys(values).forEach(key => {
    values[key] = 3;
  });

  localStorage.setItem(
    "systemStatus",
    JSON.stringify(values)
  );

  renderApp();
}

renderApp();

</script>

</body>
</html>
