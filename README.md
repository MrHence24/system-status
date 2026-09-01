# system-status
Indicates how I am today. 
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
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
  font-size: 18px;
  margin-bottom: 10px;
}

.bar {
  height: 18px;
  background: #333;
  border-radius: 10px;
  overflow: hidden;
}

.fill {
  height: 100%;
  border-radius: 10px;
}

.sens { width: 60%; background: #ff9f0a; }
.hp { width: 75%; background: #30d158; }
.energy { width: 50%; background: #0a84ff; }
.social { width: 60%; background: #bf5af2; }
.executive { width: 50%; background: #ff375f; }

button {
  width: 100%;
  padding: 15px;
  border: none;
  border-radius: 14px;
  background: #fff;
  color: #000;
  font-size: 17px;
  font-weight: bold;
  margin-top: 10px;
}
</style>
</head>

<body>

<h1>🧠 System Status</h1>

<div class="status">
  <div class="label">
    <span>Sensory Sensitivity</span>
    <span>60%</span>
  </div>
  <div class="bar"><div class="fill sens"></div></div>
</div>

<div class="status">
  <div class="label">
    <span>Body HP</span>
    <span>75%</span>
  </div>
  <div class="bar"><div class="fill hp"></div></div>
</div>

<div class="status">
  <div class="label">
    <span>Energy</span>
    <span>50%</span>
  </div>
  <div class="bar"><div class="fill energy"></div></div>
</div>

<div class="status">
  <div class="label">
    <span>Social Energy</span>
    <span>60%</span>
  </div>
  <div class="bar"><div class="fill social"></div></div>
</div>

<div class="status">
  <div class="label">
    <span>Executive Function</span>
    <span>50%</span>
  </div>
  <div class="bar"><div class="fill executive"></div></div>
</div>

</body>
</html>
