<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Weather App</title>
        <link rel="stylesheet" href="styles.css">
    </head>
    <body>

        <div class="weather-container">
            <div class="weather-card">
                <div class="weather-header">
                    <h1>Weather App</h1>
                </div>

                <div class="weather-body">
                    <!-- Location Input -->
                    <div class="location">
                        <input type="text" id="location-input"
                            placeholder="Enter City" />
                        <button id="get-weather">Get Weather</button>
                    </div>

                    <!-- Weather Information -->
                    <div class="weather-info">
                        <h2 id="location-name">City, Country</h2>
                        <div class="temperature">
                            <h3 id="temp">-- °C</h3>
                            <p id="weather-type">--</p>
                        </div>
                        <div class="additional-info">
                            <p id="humidity">Humidity: --</p>
                            <p id="wind-speed">Wind: -- km/h</p>
                        </div>
                    </div>

                </div>

                <div class="weather-footer">
                    <p>&#169; 2024 Weather App</p>
                </div>
            </div>
        </div>

        <script src="script.js"></script>
    </body>
</html>



/* General Reset */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  
  body {
    font-family: Arial, sans-serif;
    background-color: #f4f6f9;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-image: url('https://source.unsplash.com/1600x900/?sky,weather'); /* Background image */
    background-size: cover;
    background-position: center;
  }
  
  /* Weather Container */
  .weather-container {
    width: 100%;
    max-width: 400px;
    background: rgba(255, 255, 255, 0.8);
    border-radius: 15px;
    padding: 30px;
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.1);
  }
  
  /* Weather Card */
  .weather-card {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  
  /* Header */
  .weather-header {
    text-align: center;
    margin-bottom: 20px;
  }
  
  .weather-header h1 {
    font-size: 2rem;
    color: #333;
  }
  
  /* Location Input Section */
  .location {
    display: flex;
    justify-content: space-between;
    width: 100%;
    margin-bottom: 20px;
  }
  
  .location input {
    width: 75%;
    padding: 10px;
    border-radius: 5px;
    border: 1px solid #ddd;
    font-size: 1rem;
  }
  
  .location button {
    padding: 10px 15px;
    background-color: #3498db;
    border: none;
    border-radius: 5px;
    color: white;
    font-size: 1rem;
    cursor: pointer;
  }
  
  .location button:hover {
    background-color: #2980b9;
  }
  
  /* Weather Information */
  .weather-info {
    text-align: center;
  }
  
  .weather-info h2 {
    font-size: 1.5rem;
    margin-bottom: 10px;
    color: #333;
  }
  
  .temperature h3 {
    font-size: 3rem;
    color: #3498db;
  }
  
  .temperature p {
    font-size: 1.2rem;
    color: #555;
  }
  
  /* Additional Info */
  .additional-info {
    font-size: 1rem;
    color: #555;
  }
  
  .additional-info p {
    margin: 5px 0;
  }
  
  /* Footer */
  .weather-footer {
    text-align: center;
    margin-top: 20px;
    font-size: 0.8rem;
    color: #aaa;
  }



  // const apiKey = 'e3b6282e97195a6fc117d4d7943b1414';  

// // Function to fetch weather data from OpenWeatherMap API
// const getWeather = async (city) => {
//   const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric`;
//   try {
//     const response = await fetch(url);
//     const data = await response.json();
//     if (data.cod === "404") {
//       alert("City not found!");
//     } else {
//       // Display weather data
//       document.getElementById('location-name').textContent = `${data.name}, ${data.sys.country}`;
//       document.getElementById('temp').textContent = `${data.main.temp}°C`;
//       document.getElementById('weather-type').textContent = data.weather[0].description;
//       document.getElementById('humidity').textContent = `Humidity: ${data.main.humidity}%`;
//       document.getElementById('wind-speed').textContent = `Wind: ${data.wind.speed} km/h`;
//     }
//   } catch (error) {
//     alert('Error fetching weather data');
//   }
// };

// // Event listener for the "Get Weather" button
// document.getElementById('get-weather').addEventListener('click', () => {
//   const city = document.getElementById('location-input').value;
//   if (city) {
//     getWeather(city);
//   } else {
//     alert("Please enter a city name");
//   }
// });

// // Optional: Add event listener for pressing 'Enter' to get the weather
// document.getElementById('location-input').addEventListener('keypress', (e) => {
//   if (e.key === 'Enter') {
//     const city = document.getElementById('location-input').value;
//     if (city) {
//       getWeather(city);
//     } else {
//       alert("Please enter a city name");
//     }
//   }
// });
function getweather(){
    const apikey = 'e3b6282e97195a6fc117d4d7943b1414';
    const city = document.getElementById('city').value;

    if (!city){
        alert('Please enetr a city');
        return;
    }
    const currentWeatherUrl = 'https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}';
    const forecastUrl = 'https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}';

    fetch(currentWeatherUrl)
        .then(response => response.json())
        .then(data => {
            displayWeather(data);
        })
        .catch(error => {
            console.error('Error fetching current weather data:' , error);
            alert('Error fetching current weather data. Please try again.');
        });

        fetch(forecastUrl)
        .then(response => response.json())
        .then(data => {
            displayHourlyforecast(data.list);
        })
        .catch(error => {
            console.error('Error fetching current weather data:' , error);
            alert('Error fetching current weather data. Please try again.');
        });  
}
function displayWeather(data){
    const tempDivinfo = document.getElementById('temp-div');
    const weatherInfoDiv = document.getElementById('weather-info');
    const weatherIcon = document.getElementById('weather-icon');
    const hourlyforecastDiv = document.getElementById('hourly-forecast');

    weatherInfoDiv.innerHTML = '';
    hourlyforecastDiv.innerHTML = '';
    tempDivinfo.innerHTML = '';

    if (data.cod === '404'){
        weatherInfoDiv.innerHTML = '<p>${data.message}</p>';
    }else{
        const cityName = data.name;
        const Temperature = Math.round(data.main.temp -273.15);
        const description = data.weather[0].description;
        const iconCode = data.weather[0].icon;
        const iconUrl = 'https://openweathermap.org/img/wn/${iconCode}@4x.png';
        const temperatureHTML = '
            <p>${temperature}°C</p>';
        const weatherHTML = '<p>${cityName}</p>';
       
        tempDivinfo.innerHTML = temperatureHTML;
        weatherInfoDiv.innerHTML = weatherHTML;
        weatherIcon.src = iconUrl;
        weather.alt = description;

        showImage();
}
function displayHourlyforecast(hourlyData){
    const hourlyforecastDiv = document.getElementById('hourly-forecast');
    const next24Hours = hourlyData.slice(0, 8);
    next24Hours.forEach(item => {
        const dateTime = new Date(item.dt * 1000);
        const hour = dateTime.getHours();
        const temperature = math.round(item.main.temp - 273.15);
        const iconCode = item.weather[0].icon;
        const iconUrl = 'https://openweathermap.org/img/wn/${iconCode}.png';

        const hourlyItemHtml = 
        <div class="hourly-item">
        <span>${hour}:00</span>
        <img src="${iconUrl}" alt= "Hourly Weather Icon">
            <span>${temperature}°C</span>
            </div>
        ;
            hourlyforecastDiv.innerHTML += hourlyItemHtml;
    });
function showImage(){
    const weatherIcon = document.getElementById('weather-icon');
    weatherIcon.style.display = 'block';

}
}
}

