<!DOCTYPE html>
<html lang="pl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Basen Zawadzkie</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
      background: #f0f8ff;
      color: #333;
      line-height: 1.6;
    }
    h1 {
      font-size: 24px;
      font-weight: bold;
      margin-bottom: 20px;
    }
    .section {
      margin-bottom: 16px; /* odstęp 1 linijki */
    }
    .footer {
      margin-top: 24px;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <h1>Basen Zawadzkie</h1>

  <div class="section">
    <strong>Status:</strong><br />🔥 - nieczynne
  </div>
  
  <div class="section">
    <strong>Dane pogodowe - Zawadzkie:</strong><br />
    🕐: <span id="weather-time">--:--</span><br />
    🌡️: <span id="temperature">--°C</span><br />
    ☁️: <span id="cloudiness">--</span><br />
    🌧️: opady: <span id="precipitation">--</span>
  </div>

  <div class="section">
    <strong>Basen duży:</strong><br />
    🕐: 13:00<br />
    🌡️💧: 24°C<br />
  </div>

  <div class="section">
    <strong>Basen mały:</strong><br />
    🕐: 13:00<br />
    🌡️💧: 26°C<br />
  </div>

  <div class="section">
    <strong>Prognoza na następny dzień:</strong><br />🔴 - nieczynne
  </div>

  <div class="section">
    <strong>Informacje dodatkowe:</strong><br />
    Brak
  </div>

  <div class="footer">
    Ratownik: <strong>Dawid Szramek</strong>
  </div>

  <script>
    // Funkcja do aktualizacji godziny
    function updateTime() {
      const now = new Date();
      const hours = now.getHours().toString().padStart(2, "0");
      const minutes = now.getMinutes().toString().padStart(2, "0");
      document.getElementById("weather-time").textContent = `${hours}:${minutes}`;
    }

    updateTime();
    setInterval(updateTime, 60000); // aktualizacja co minutę

    // Funkcja do pobierania danych pogodowych z WeatherAPI
    async function getWeather() {
      const apiKey = "bba4586a8e424e6cbf3125210251904"; // Twój klucz API
      const city = "Zawadzkie"; // Miasto
      const url = `https://api.weatherapi.com/v1/current.json?key=${apiKey}&q=${city}&lang=pl`; // URL do API

      try {
        const response = await fetch(url);
        
        // Jeśli odpowiedź jest OK, parsuj dane
        if (response.ok) {
          const data = await response.json();
          const temperature = data.current.temp_c;
          const cloudiness = data.current.condition.text;
          const precipitation = data.current.precip_mm;
          const precipitationText = precipitation > 0 ? "występują" : "nie występują";

          document.getElementById("temperature").textContent = `${temperature}°C`;
          document.getElementById("cloudiness").textContent = cloudiness;
          document.getElementById("precipitation").textContent = precipitationText;
        } else {
          console.error('Błąd: Nie udało się pobrać danych pogodowych');
        }
      } catch (error) {
        console.error("Błąd przy pobieraniu danych pogodowych:", error);
      }
    }

    getWeather();
  </script>
</body>
</html>
