# weather
mport requests

def get_weather(api_key, city):
    url = f'http://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}&units=metric'
    response = requests.get(url)
    data = response.json()

    if response.status_code == 200:
        weather_description = data['weather'][0]['description']
        temperature = data['main']['temp']
        humidity = data['main']['humidity']
        wind_speed = data['wind']['speed']
        return weather_description, temperature, humidity, wind_speed
    else:
        return None

def main():
    api_key = 'YOUR_API_KEY'
    city = input("Enter city name: ")

    weather_info = get_weather(api_key, city)

    if weather_info:
        description, temperature, humidity, wind_speed = weather_info
        print(f"Weather in {city}:")
        print(f"Description: {description}")
        print(f"Temperature: {temperature}°C")
        print(f"Humidity: {humidity}%")
        print(f"Wind Speed: {wind_speed} m/s")
    else:
        print("Failed to retrieve weather information.")

if __name__ == "__main__":
    main()