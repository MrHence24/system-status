# system-status
Indicates how I am today. 
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">

<title>System Status</title>

<style>
body {
  margin: 0;
  padding: 20px;
  background: #111;
  color: white;
  font-family: -apple-system, BlinkMacSystemFont, sans-serif;
}

h1 {
  text-align: center;
  margin-bottom: 25px;
}

.status {
  background: #1d1d1f;
  border-radius: 18px;
  padding: 18px;
  margin-bottom: 15px;
}

.label {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 18px;
  margin-bottom: 12px;
}

.percent {
  font-weight: bold;
}

.bar {
  height: 18px;
  background: #333;
  border-radius: 10px;
  overflow: hidden;
  margin-bottom: 15px;
}

.fill {
  height: 100%;
  border-radius: 10px;
  transition: width 0.2s;
}

.controls {
  display: flex;
  gap: 10px;
}

button {
  flex: 1;
  border: none;
  border-radius: 12px;
  padding: 12px;
  font-size: 22px;
  font-weight: bold;
  background: #333;
  color: white;
}

button:active {
  transform: scale(0.95);
}

.sens { background: #ff9f0a; }
.hp { background: #30d158; }
.energy { background: #0a84ff; }
.social { background: #bf5af2; }
.executive { background: #ff375f; }
</style>
</head>

<body>

<h1>🧠 System Status</h1>

<div class="status">
  <div class="label">
    <span>Sensory Sensitivity</span>
    <span class="percent" id="sensory-value">60%</span>
  </div>
  <div class="bar">
    <div class="fill sens" id="sensory-bar" style="width:60%"></div>
  </div>
  <div class="controls">
    <button onclick="change('sensory', -10)">−</button>
    <button onclick="change('sensory', 10)">+</button>
  </div>
</div>

<div class="status">
  <div class="label">
    <span>Body HP</span>
    <span class="percent" id="hp-value">75%</span>
  </div>
  <div class="bar">
    <div class="fill hp" id="hp-bar" style="width:75%"></div>
  </div>
  <div class="controls">
    <button onclick="change('hp', -10)">−</button>
    <button onclick="change('hp', 10)">+</button>
  </div>
</div>

<div class="status">
  <div class="label">
    <span>Energy</span>
    <span class="percent" id="energy-value">50%</span>
  </div>
  <div class="bar">
    <div class="fill energy" id="energy-bar" style="width:50%"></div>
  </div>
  <div class="controls">
    <button onclick="change('energy', -10)">−</button>
    <button onclick="change('energy', 10)">+</button>
  </div>
</div>

<div class="status">
  <div class="label">
    <span>Social Energy</span>
    <span class="percent" id="social-value">60%</span>
  </div>
  <div class="bar">
    <div class="fill social" id="social-bar" style="width:60%"></div>
  </div>
  <div class="controls">
    <button onclick="change('social', -10)">−</button>
    <button onclick="change('social', 10)">+</button>
  </div>
</div>

<div class="status">
  <div class="label">
    <span>Executive Function</span>
    <span class="percent" id="executive-value">50%</span>
  </div>
  <div class="bar">
    <div class="fill executive" id="executive-bar" style="width:50%"></div>
  </div>
  <div class="controls">
    <button onclick="change('executive', -10)">−</button>
    <button onclick="change('executive', 10)">+</button>
  </div>
</div>

<script>

let values = {
  sensory: 60,
  hp: 75,
  energy: 50,
  social: 60,
  executive: 50
};

function change(name, amount) {

  values[name] += amount;

  if (values[name] < 0) values[name] = 0;
  if (values[name] > 100) values[name] = 100;

  document.getElementById(name + "-value").textContent =
    values[name] + "%";

  document.getElementById(name + "-bar").style.width =
    values[name] + "%";
}

</script>

</body>
</html>
