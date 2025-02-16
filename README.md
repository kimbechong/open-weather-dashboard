# open-weather-dashboard

## Table of Contents

- [Description](#description)
- [Tech Stack](#tech-stack)
- [Data](#data)
- [Project Status](#project-status)
    - [To Do](#to-do)
- [Installation](#installation)

## Description

This web application provides current weather data when users search by city name. It calls OpenWeather APIs for city geolocation and weather data.

## Tech Stack

-   [VueJS](https://vuejs.org/)
-   [Vite](https://vite.dev/)
-   [Pure.css](https://pure-css.github.io/)

## Data
-   [OpenWeather API](https://openweathermap.org/api)
    -   [OpenWeather API Postman Collection](https://www.postman.com/kimbechong/workspace/kimbechong/collection/15185265-3ac01b40-4463-49c8-b5a0-c6f6bbb88e15?action=share&creator=15185265)

## Project Status

🚧 In Progress

### To Do

-   [ ] Add styling
    -   use OpenWeather API color scheme (orange, gray, black)
-   [ ] Programmable API Key
-   [ ] Include link to Postman collection
-   [ ] Add screenshots to `README.md`
-   [ ] Add features in `README.md`
-   [ ] Allow users to select city if there's multiple matching options
-   [ ] Allow users to save city to dashboard
-   [ ] Dark mode toggle

## Installation

1. Clone the repository

```shell
git clone git@github.com:kimbechong/weather-dashboard.git
```

2. Navigate to the project directory

```shell
cd weather-dashboard
```

3. Install dependencies

```shell
npm install
```

4. Start the project locally

```shell
npm run dev
```

5. Navigate to `http://localhost:5173/` on your browser
