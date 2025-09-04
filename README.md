# Pawcast - Dog Walking Weather App for Tidbyt

A Tidbyt app that helps dog owners determine safe walking conditions based on current weather data. Pawcast displays temperature, humidity, heat index, and provides risk assessments for walking dogs in hot weather.

## Features

- **Real-time weather data** from OpenWeatherMap API
- **Heat index calculation** to assess actual "feels like" temperature
- **Risk assessment** with color-coded warnings (Low, Moderate, High, Extreme)
- **Walk duration recommendations** based on risk level
- **Clean, readable display** optimized for Tidbyt's low-resolution screen

## Installation

### Prerequisites

1. **Tidbyt device** - You'll need a physical Tidbyt device to display the app
2. **Pixlet CLI** - Install the Tidbyt development tools:
   ```bash
   brew install tidbyt/tidbyt/pixlet
   ```

### Setup

1. **Clone this repository:**
   ```bash
   git clone https://github.com/yourusername/pawcast.git
   cd pawcast
   ```

2. **Get an OpenWeatherMap API key:**
   - Sign up at [OpenWeatherMap](https://openweathermap.org/api)
   - Get your free API key
   - Add it to your Tidbyt device settings

3. **Install on your Tidbyt:**
   ```bash
   pixlet push your-device-id pawcast.star
   ```

## Configuration

The app uses the following configuration options in your Tidbyt device settings:

- `api_key`: Your OpenWeatherMap API key
- `zip_code`: Your location's ZIP code (US only)
- `units`: Temperature units (`imperial` for Fahrenheit, `metric` for Celsius)

## Local Development

To test the app locally:

```bash
# Render a static frame
pixlet render pawcast.star

# Start a local preview server
pixlet serve pawcast.star --host 127.0.0.1 --port 8080
```

Then visit `http://127.0.0.1:8080` in your browser to see the preview.

## How It Works

Pawcast fetches current weather data and calculates the heat index using the formula:
```
Heat Index = -42.379 + 2.04901523*T + 10.14333127*R - 0.22475541*T*R - 6.83783*10^-3*T^2 - 5.481717*10^-2*R^2 + 1.22874*10^-3*T^2*R + 8.5282*10^-4*T*R^2 - 1.99*10^-6*T^2*R^2
```

Where:
- T = Temperature in Fahrenheit
- R = Relative humidity percentage

The app then categorizes the risk level:
- **Low (Green)**: Heat index < 80°F - Safe for normal walks
- **Moderate (Yellow)**: Heat index 80-90°F - Limit exercise, provide water
- **High (Orange)**: Heat index 90-103°F - Short walks only, avoid midday
- **Extreme (Red)**: Heat index > 103°F - Avoid outdoor exercise

## Contributing

Feel free to submit issues and enhancement requests!

## License

This project is open source and available under the [MIT License](LICENSE).

## Acknowledgments

- Weather data provided by [OpenWeatherMap](https://openweathermap.org/)
- Built for [Tidbyt](https://tidbyt.com/) display devices