# weather
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Weather App</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(to right, #83a4d4, #b6fbff);
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }

    .weather-app {
      background-color: white;
      padding: 30px 40px;
      border-radius: 10px;
      box-shadow: 0 0 15px rgba(0,0,0,0.1);
      text-align: center;
      max-width: 400px;
      width: 100%;
    }

    input {
      padding: 10px;
      width: 70%;
      border: 1px solid #ccc;
      border-radius: 5px;
      margin-right: 10px;
    }

    button {
      padding: 10px 15px;
      border: none;
      background-color: #3498db;
      color: white;
      border-radius: 5px;
      cursor: pointer;
    }

    button:hover {
      background-color: #2980b9;
    }

    .result {
      margin-top: 20px;
      font-size: 18px;
    }
  </style>
</head>
<body>
  <div class="weather-app">
    <h1>Weather App</h1>
    <form id="weatherForm">
      <input type="text" id="locationInput" placeholder="Enter location" required />
      <button type="submit">Get Weather</button>
    </form>
    <div class="result" id="weatherResult"></div>
  </div>

  <script>
    document.getElementById('weatherForm').addEventListener('submit', function(e) {
      e.preventDefault();

      const location = document.getElementById('locationInput').value;
      const resultDiv = document.getElementById('weatherResult');
      const apiKey = '0c4a189b36f543fb8a595948251308';
      const url = `https://api.weatherapi.com/v1/current.json?key=${apiKey}&q=${encodeURIComponent(location)}&aqi=yes`;

      resultDiv.innerHTML = 'Loading...';

      fetch(url)
        .then(response => {
          if (!response.ok) {
            throw new Error('Location not found');
          }
          return response.json();
        })
        .then(data => {
          const tempC = data.current.temp_c;
          const condition = data.current.condition.text;
          const city = data.location.name;
          const country = data.location.country;

          resultDiv.innerHTML = `
            <strong>${city}, ${country}</strong><br>
            Temperature: ${tempC}°C<br>
            Condition: ${condition}
          `;
        })
        .catch(error => {
          resultDiv.innerHTML = `Error: ${error.message}`;
        });
    });
  </script>
</body>
</html>
