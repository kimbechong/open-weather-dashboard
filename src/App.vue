<template>
	<!-- get weather by searching city -->
	<WeatherSearch
		:weather-data="weatherData"
		@update-weather-data="updateWeatherData"
		@unit-button-click="switchUnit"
	/>

	<!-- display current weather -->
	<WeatherCard :weather-data="weatherData" />

	<!-- pin weather -->
</template>

<script>
import WeatherSearch from './components/WeatherSearch.vue';
import WeatherCard from './components/WeatherCard.vue';

export default {
	name: 'App',
	components: {
		WeatherSearch,
		WeatherCard,
	},
	data() {
		return {
			weatherData: {
				location: {
					city: null,
					state: '',
					country: '',
				},
				weather: {
					unit: 'imperial',
					temp: 0,
					humidity: 0,
					wind: 0,
					rain: 0,
					snow: 0,
					weatherCondition: '',
					weatherDescription: '',
					weatherIcon: '',
				},
			},
		};
	},
	methods: {
		updateWeatherData(newWeatherData) {
			this.weatherData = newWeatherData;
		},
		switchUnit() {
			if (this.weatherData.weather.unit === 'imperial') {
				this.weatherData.weather.unit = 'metric';
			} else {
				this.weatherData.weather.unit = 'imperial';
			}
		},
	},
	watch: {
		'weatherData.weather.unit'(unit) {
			console.log(unit);
			let temp = this.weatherData.weather.temp;
			if (unit === 'imperial') {
				temp = (temp - 32) * (5 / 9);
			} else {
				temp = temp * (9 / 5) + 32;
			}
			console.log('temp: ' + temp);
		},
	},
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100..900;1,100..900&display=swap');

#app {
	font-family: Montserrat, serif;
	font-style: normal;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #48484a;
	margin-top: 60px;
}
</style>
