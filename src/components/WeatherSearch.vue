<template>
	<div>
		<h1>Weather Dashboard</h1>
		<form class="pure-form">
			<input
				id="city-input"
				class="pure-input-2-3"
				type="text"
				v-model="city"
				placeholder="Enter City Name"
			/>
			<button
				id="searchCity"
				class="pure-button pure-button-primary"
				type="button"
				@click="getCurrentWeather"
			>
				Search
			</button>
		</form>
		<!-- features: allow use to pick city if multiple with same name -->

		<!-- to do: show 2 buttons for units and disable selected unit -->
		<button
			id="changeUnit"
			class="pure-button"
			type="button"
			@click="handleUnitButtonClick"
		>
			{{ weatherData.weather.unit === 'imperial' ? '°F' : '°C' }}
		</button>
	</div>
</template>

<script>
import axios from 'axios';

export default {
	name: 'WeatherSearch',
	props: {
		weatherData: {
			type: Object,
			required: true,
		},
	},
	data() {
		return {
			apiKey: '',
			lat: 0,
			lon: 0,
			city: '',
			state: '',
			country: '',
			temp: 0,
			humidity: 0,
			wind: 0,
			rain: 0,
			snow: 0,
			weatherCondition: '',
			weatherDescription: '',
			weatherIcon: '',
		};
	},
	methods: {
		async getCurrentWeather() {
			this.apiKey = import.meta.env.VITE_API_KEY;
			console.log('VITE_API_KEY: ' + this.apiKey);
			await this.getGeocode(this.city);
			const url = `https://api.openweathermap.org/data/2.5/weather?lat=${this.lat}&lon=${this.lon}&units=${this.weatherData.weather.unit}&appId=${this.apiKey}`;
			try {
				const response = await axios.get(url);
				const data = response.data;
				// console.log(data);
				this.temp = data.main.temp;
				this.humidity = data.main.humidity;
				this.wind = data.wind.speed;
				if (data.rain) {
					this.rain = data.rain['1h'];
				}
				if (data.snow) {
					this.snow = data.snow['1h'];
				}
				this.weatherCondition = data.weather[0].main;
				this.weatherDescription = data.weather[0].description;
				this.weatherIcon = data.weather[0].icon;
			} catch (error) {
				console.error('getCurrentWeather error: ', error);
			}
			this.updateCityWeather();
		},
		// get lat and lon from city, state, country
		async getGeocode(query) {
			const url = `https://api.openweathermap.org/geo/1.0/direct?q=${query}&limit=1&appid=${this.apiKey}`;
			try {
				const response = await axios.get(url);
				const data = response.data[0];
				console.log(data);
				this.name = data.name;
				this.state = data.state;
				this.country = data.country;
				this.lat = data.lat;
				this.lon = data.lon;
				console.log('coordinates: ' + this.lat + ', ' + this.lon);
			} catch (error) {
				console.error('getGeocode error: ', error);
			}
		},
		updateCityWeather() {
			this.$emit('update-weather-data', {
				location: {
					city: this.city,
					state: this.state,
					country: this.country,
				},
				weather: {
					temp: this.temp,
					humidity: this.humidity,
					wind: this.wind,
					rain: this.rain,
					snow: this.snow,
					weatherCondition: this.weatherCondition,
					weatherDescription: this.weatherDescription,
					weatherIcon: this.weatherIcon,
				},
			});
		},
		handleUnitButtonClick() {
			this.$emit('unit-button-click');
		},
	},
	emits: ['update-weather-data', 'unit-button-click'],
};
</script>

<style scoped>
#city-input {
	margin: 10px;
}

#searchCity {
	background-color: #ED6E4C;
	color: #F2F2F1;
}

#changeUnit {
	background-color: #88C5EB;;
	color: #48484A;
}
</style>
