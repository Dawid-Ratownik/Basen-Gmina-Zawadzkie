# Basen-Gmina-Zawadzkie
<!DOCTYPE html>
<html lang="pl">
<head>
    <strong>🕐:</strong> <span id="current-time">--:--</span><br />
    <strong>Status:</strong><br />🔴 - nieczynne
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
    🧪💧: 1.0 Chlor<br />
    ⚖️💧: 7.2 pH
  </div>

  <div class="section">
    <strong>Basen mały:</strong><br />
    🕐: 13:00<br />
    🌡️💧: 26°C<br />
    🧪💧: 0.9 Chlor<br />
    ⚖️💧: 7.3 pH
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
    function updateTime() {
      const now = new Date();
      const hours = now.getHours().toString().padStart(2, "0");
      const minutes = now.getMinutes().toString().padStart(2, "0");
      document.getElementById("current-time").textContent = `${hours}:${minutes}`;
      document.getElementById("weather-time").textContent = `${hours}:${minutes}`;
    }

    updateTime();
    setInterval(updateTime, 60000);

    async function getWeather() {
      const apiKey = "bba4586a8e424e6cbf3125210251904";
      const city = "Zawadzkie";
      const url = `https://api.weatherapi.com/v1/current.json?key=${apiKey}&q=${city}&lang=pl`;

      try {
        const response = await fetch(url);
        const data = await response.json();

        const temperature = data.current.temp_c;
        const cloudiness = data.current.condition.text;
        const precipitation = data.current.precip_mm;
        const precipitationText = precipitation > 0 ? "występują" : "nie występują";

        document.getElementById("temperature").textContent = `${temperature}°C`;
        document.getElementById("cloudiness").textContent = cloudiness;
        document.getElementById("precipitation").textContent = precipitationText;
      } catch (error) {
        console.error("Błąd przy pobieraniu danych pogodowych:", error);
      }
    }

    getWeather();
  </script>
</body>
</html>
