# -weather-app
import requests

class WeatherForecast:
    def __init__(self, api_key):
        self.api_key = api_key

    def get_weather(self, city):
        url = f"http://api.openweathermap.org/data/2.5/weather?q={city}&appid={self.api_key}&units=metric"
        response = requests.get(url)
        data = response.json()
        return data

# Example usage
api_key = "your_api_key"
weather_forecast = WeatherForecast(api_key)
city = "London"
weather_data = weather_forecast.get_weather(city)

if weather_data["cod"] == 200:
    print(f"Weather forecast for {city}:")
    print(f"Temperature: {weather_data['main']['temp']}°C")
    print(f"Description: {weather_data['weather'][0]['description']}")
else:
    print(f"Failed to fetch weather forecast for {city}. Error code: {weather_data['cod']}")
