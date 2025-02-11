<template>
	<div class="weather-card" v-if="weatherData.location.city">
		<h2>Weather Information</h2>
		<p>{{ weatherData.location.city }}, {{ weatherData.location.state }}, {{ weatherData.location.country }}</p>
		<p>Temperature: {{ weatherData.weather.temp }}°</p>
		<p>Humidity: {{ weatherData.weather.humidity }}%</p>
		<p>Wind: {{ weatherData.weather.wind }}</p>
		<p>Condition: {{ weatherData.weather.weatherCondition }}</p>
		<p>Description: {{ weatherData.weather.weatherDescription }}</p>
		<img
			:src="`http://openweathermap.org/img/wn/${weatherData.weather.weatherIcon}@2x.png`"
			alt="Weather Icon"
		/>
	</div>
</template>

<script>
export default {
	name: 'WeatherCard',
	props: {
		weatherData: {
			type: Object,
			required: true,
		},
	},
};
</script>

<style scoped>
.weather-card {
	border: 1px solid #ccc;
	padding: 16px;
	border-radius: 8px;
	text-align: center;
}
</style>
