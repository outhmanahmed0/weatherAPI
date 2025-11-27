<script>
  

  let weatherData = null;
  let loading = true;
  let error = null;


  const latitude = 33.3152;
  const longitude = 44.3661;

  const fetchWeather = async () => {
    try {
      const url = `https://api.open-meteo.com/v1/forecast?latitude=${latitude}&longitude=${longitude}&current_weather=true`;
      const response = await fetch(url);
      const data = await response.json();

      weatherData = data.current_weather;
    } catch (err) {
      error = "error 404";
    } finally {
      loading = false;
    }
  };

  fetchWeather();
</script>


<main>
  <h1>By Othman Ahmed</h1>
  <div class="card">
    {#if loading}
      <p>🔄 Loading ...</p>
    {:else if error}
      <p class="err">{error}</p>
    {:else}
      <h2>🌤 Baghdad weather now</h2>

      <div class="temp">{weatherData.temperature}°C</div>

      <div class="details">
        <p>💨 Wind speed: {weatherData.windspeed} km/h</p>
        <p>🧭 Wind direction: {weatherData.winddirection}°</p>
      </div>
    {/if}
  </div>
</main>

<style>
@import url('https://fonts.googleapis.com/css2?family=Indie+Flower&display=swap');

h1{
  color: black;
  font-family: "Indie Flower", cursive;
  font-weight: 400;
  font-style: normal;
  animation: fadeIn 0.8s ease-in-out;
} 
 
main {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
  font-family: "Segoe UI", sans-serif;
}


.card {
  background: white;
  padding: 25px;
  border-radius: 16px;
  width: 320px;
  box-shadow: 0 10px 25px rgba(0,0,0,0.15);
  text-align: center;
  animation: fadeIn 0.8s ease-in-out;
}


h2 {
  margin-bottom: 10px;
  color: #333;
}


.temp {
  font-size: 48px;
  font-weight: bold;
  margin: 15px 0;
  color: #0077ff;
}


.details {
  margin: 10px 0;
  color: #444;
  line-height: 1.7;
  font-size: 18px;
}


.err {
  color: red;
  font-weight: bold;
}


@keyframes fadeIn {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}
</style>