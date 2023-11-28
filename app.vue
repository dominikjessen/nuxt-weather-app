<script setup lang="ts">
import type { WeatherForecast } from './types/weather';

const location = ref('')
const forecast = ref<WeatherForecast | null>()

const route = useRoute()
const locationQuery = route.query.location ? route.query.location as string : null

if (locationQuery) {
  const latLong = locationQuery.split(',') ?? null
  if (latLong) {
    const timezone = 'timezone=auto';
    const forecast_days = 'forecast_days=10';
    const current =
      'current=weather_code,temperature_2m,precipitation,apparent_temperature,wind_speed_10m,relative_humidity_2m';
    const daily = 'daily=weather_code,temperature_2m_max,temperature_2m_min';

    const { data } = await useFetch<WeatherForecast>(`https://api.open-meteo.com/v1/forecast?latitude=${latLong[0]}&longitude=${latLong[1]}&${timezone}&${current}&${daily}&${forecast_days}`)
    forecast.value = data.value ? data.value : null
  }
} else {
  forecast.value = null
}

</script>

<template>
  <div>

    <div v-if="location">Weather <span>{{ location === 'Your City' ? 'at' : 'in' }}</span> {{ location }}</div>
    <button @click="$event => location = 'Your City'">Change location</button>

    <span v-if="forecast?.current">Current Forecast temp: {{ forecast.current?.temperature_2m }} C</span>
    <span v-if="forecast?.daily">Tomorrow's Forecast temp: {{ forecast.daily.temperature_2m_max[1] }} C</span>

  </div>
</template>
