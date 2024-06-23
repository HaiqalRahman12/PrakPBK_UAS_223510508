<template>
  <div class="weather">
    <q-page class="column items-center justify-center q-pa-md">
      <div class="input-section">
        <q-input v-model="newLocation" label="Enter Location" >
        <template v-slot:prepend>
          <q-icon name="place" />
        </template>
        <template v-slot:append>
          <q-btn @click="addWeatherWidget" label="Add Widget" color="skyblue" />
        </template>
      </q-input>
      </div>
      
      
      <div class="widgets-section">
        <div
          v-for="(weather, index) in weatherStore.weatherWidgets"
          :key="index"
          class="weather-widget"
        >
        <div class="timestamp">
          <p>{{ weather.name }}, {{ weather.sys.country }}</p>
          <i class="fas fa-clock"></i> {{ formatTimestamp(new Date()) }}
          <p>{{  }}</p>
          </div>
          <div class="header">

            <div class="temp-icon">
              <q-icon :name="getWeatherIcon(weather.weather[0].main)" size="100px" />
              <h1>{{ weather.main.temp }}°C</h1><br>
              <div class="details">
                <h2>{{ weather.weather[0].description }}</h2>
                <p>Terasa seperti {{ weather.main.feels_like }}°</p>
              </div>
            </div>
          </div>
          <p style="font-size: medium;">Detail :</p>
          <div class="additional-info">
            <div class="detail-item">
              <i class="fas fa-wind"></i>
              <p>Angin: <br> {{ weather.wind.speed }} km/j</p>
            </div>
            <div class="detail-item">
              <i class="fas fa-tint"></i>
              <p>Kelembapan: <br> {{ weather.main.humidity }}%</p>
            </div>
            <div class="detail-item">
              <i class="fas fa-tachometer-alt"></i>
              <p>Tekanan: <br> {{ weather.main.pressure }} mb</p>
            </div>
            <div class="detail-item">
              <i class="fas fa-thermometer-half"></i>
              <p>Titik embun: <br> {{ convertTemp(weather.main.temp) }}</p>
            </div>
          </div>
          <center><q-btn
            @click="removeWidget(index)"
            label="Hilangkan berita"
            color="negative"
          /></center>
        </div>
      </div>
    </q-page>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { QPage, QInput, QBtn, QIcon } from "quasar";
import { useWeatherStore } from "../stores/weatherStore";

const weatherStore = useWeatherStore();

const newLocation = ref("");

const weatherIconMapping = {
  Clear: "wb_sunny",
  Clouds: "cloud",
  Rain: "grain",
  Drizzle: "grain",
  Thunderstorm: "flash_on",
  Snow: "ac_unit",
  Mist: "blur_on",
  Smoke: "blur_on",
  Haze: "blur_on",
  Dust: "blur_on",
  Fog: "blur_on",
  Sand: "blur_on",
  Ash: "blur_on",
  Squall: "blur_on",
  Tornado: "toys",
};

const convertTemp = (tempInCelsius) => {
  return `${tempInCelsius.toFixed(1)}°C / ${(
    (tempInCelsius * 9) / 5 +
    32
  ).toFixed(1)}°F`;
};

const getWeatherIcon = (weatherMain) => {
  return weatherIconMapping[weatherMain] || "wb_cloudy";
};

const addWeatherWidget = async () => {
  await weatherStore.fetchWeather(newLocation.value);
  newLocation.value = "";
};

const removeWidget = (index) => {
  weatherStore.removeWidget(index);
};

const formatTimestamp = (date) => {
  return date.toLocaleString();
};
</script>

<style scoped>
.weather {
  background: linear-gradient(to right, #6dd5ed, #87ceeb);
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #fff;
}

.input-section {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
  margin-bottom: 20px;
}

.widgets-section {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
}

.weather-widget {

  padding: 20px;
  border-radius: 10px;
  text-align: left;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  width: auto;
  color: #fff;
}



.weather-widget .temp-icon {
  display: flex;
  align-items: center;
  gap: 5px;
}

.weather-widget .temp-icon h1 {
  margin-left: 10px;
  font-size: 50px;
}

.weather-widget .details {
  text-align: left;
  line-height: 1px;
}

.weather-widget .details h2 {
  font-size: 2.2em;
  margin: 0;
}


.timestamp {
  margin-top: 5px;
  line-height:2px;

  font-size: 15px;
}

.timestamp p{
  font-size: 20px;
}


.weather-widget .additional-info {
  margin-top: 20px;
  display: flex;
  justify-content: space-between;
}

.weather-widget .detail-item {
  text-align: center;
}

.weather-widget .detail-item i {
  display: block;
  font-size: 1.5em;
  margin-bottom: 5px;
}
</style>
