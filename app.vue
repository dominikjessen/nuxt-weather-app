<script setup lang="ts">
import type { WeatherForecast } from './types/weather';

const isLoading = ref(false)
const location = ref('')
const forecast = ref<WeatherForecast | null>()

const route = useRoute()

// Watch for location query changes on the route
watch(route, async () => {
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
})

function locationChanged(newLocation: string) {
  location.value = newLocation;
  isLoading.value = false;
}

useHead({
  title: 'Nuxt Weather App',
  meta: [
    { name: 'description', content: 'Get the current weather forecast' }
  ],
  bodyAttrs: {
    class: computed(() => 'min-h-screen bg-slate-50 text-slate-900'),
  },
});
</script>

<template>
  <LoadingOverlay v-if="isLoading" />
  <div class="flex flex-col gap-4 lg:gap-8 items-center justify-center w-11/12 md:w-4/5 mx-auto py-4">
    <h1 class="text-2xl font-bold">Check the weather in...</h1>
    <Search @location-changed="locationChanged" @start-transition="isLoading = true" />
    <h2 v-if="location" class="font-bold text-xl md:text-2xl">
      <span>Weather</span><span>{{ location === 'Your Location' ? ' at ' : ' in ' }}</span><span>{{ location }}</span>
    </h2>
    <CurrentForecast v-if="forecast?.current && forecast.current_units" :data="forecast.current"
      :units="forecast.current_units" />
    <DailyForecast v-if="forecast?.daily" :data="forecast.daily" />

  </div>
</template>
