<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Traffic Accidents Data Visualization</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0; padding: 0;
      background: #f5f5f5;
      color: #333;
    }
    header {
      background: #2c3e50;
      color: #fff;
      padding: 20px;
      text-align: center;
    }
    h1 { margin: 0; }
    .container {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
      gap: 20px;
      padding: 20px;
    }
    .card {
      background: #fff;
      padding: 15px;
      border-radius: 10px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.1);
    }
    canvas {
      width: 100% !important;
      height: 300px !important;
    }
  </style>
</head>
<body>
<header>
  <h1>🚦 Traffic Accidents Data Visualization</h1>
  <p>Interactive Dashboard (Sample Dataset)</p>
</header>

<div class="container">
  <!-- Bar Chart -->
  <div class="card">
    <h3>Accidents per Month</h3>
    <canvas id="barChart"></canvas>
  </div>

  <!-- Line Chart -->
  <div class="card">
    <h3>Accidents Trend (2019-2023)</h3>
    <canvas id="lineChart"></canvas>
  </div>

  <!-- Pie Chart -->
  <div class="card">
    <h3>Causes of Accidents</h3>
    <canvas id="pieChart"></canvas>
  </div>

  <!-- Map Style Heat Grid -->
  <div class="card">
    <h3>Accidents by Region</h3>
    <canvas id="heatMap"></canvas>
  </div>
</div>

<script>
  // Sample Dataset
  const accidentsPerMonth = [120, 150, 180, 90, 200, 250, 300, 280, 260, 220, 170, 140];
  const months = ["Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec"];

  const yearlyData = {
    years: [2019, 2020, 2021, 2022, 2023],
    values: [1200, 1400, 1100, 1800, 2000]
  };

  const causes = {
    labels: ["Over Speeding", "Drunk Driving", "Weather", "Mechanical Failure", "Others"],
    data: [40, 25, 15, 10, 10]
  };

  const regions = {
    labels: ["North", "South", "East", "West", "Central"],
    data: [300, 500, 200, 400, 350]
  };

  // Bar Chart
  new Chart(document.getElementById("barChart"), {
    type: "bar",
    data: {
      labels: months,
      datasets: [{
        label: "Number of Accidents",
        data: accidentsPerMonth,
        backgroundColor: "rgba(52, 152, 219, 0.6)",
        borderColor: "#2980b9",
        borderWidth: 1
      }]
    },
    options: {
      responsive: true,
      plugins: {
        legend: { display: false }
      },
      scales: {
        y: { beginAtZero: true }
      }
    }
  });

  // Line Chart
  new Chart(document.getElementById("lineChart"), {
    type: "line",
    data: {
      labels: yearlyData.years,
      datasets: [{
        label: "Accidents per Year",
        data: yearlyData.values,
        fill: false,
        borderColor: "#e74c3c",
        tension: 0.2
      }]
    },
    options: {
      responsive: true,
      plugins: {
        legend: { position: "top" }
      }
    }
  });

  // Pie Chart
  new Chart(document.getElementById("pieChart"), {
    type: "pie",
    data: {
      labels: causes.labels,
      datasets: [{
        data: causes.data,
        backgroundColor: [
          "#e67e22", "#c0392b", "#3498db", "#2ecc71", "#9b59b6"
        ]
      }]
    },
    options: {
      responsive: true,
      plugins: {
        legend: { position: "right" }
      }
    }
  });

  // Heat Map (Region-wise Accidents)
  new Chart(document.getElementById("heatMap"), {
    type: "bar",
    data: {
      labels: regions.labels,
      datasets: [{
        label: "Accidents by Region",
        data: regions.data,
        backgroundColor: regions.data.map(v => 
          `rgba(231,76,60,${0.3 + v/600})`
        )
      }]
    },
    options: {
      indexAxis: "y",
      scales: {
        x: { beginAtZero: true }
      },
      plugins: {
        legend: { display: false }
      }
    }
  });
</script>
</body>
</html>
