# Weather App

A modern weather application built with Nuxt 3 that provides real-time weather information for any city. Built with simplicity and user experience in mind.

## Features

- Real-time weather data using OpenWeather API
- Clean and intuitive user interface
- Display of temperature, humidity, and wind speed
- Dynamic weather icons based on current conditions
- Responsive design

## Prerequisites

Before you begin, ensure you have:
- Node.js installed (version 16.x or higher)
- An OpenWeather API key (get one at [OpenWeather](https://openweathermap.org/api))

## Setup

1. Clone the repository:
```bash
git clone https://github.com/yourusername/weather-app.git
cd weather-app
```

2. Install dependencies:
```bash
# npm
npm install

# yarn
yarn install

# pnpm
pnpm install

# bun
bun install
```

3. Environment Setup:
   - Create a `.env` file in the root directory
   - Copy the contents from `.env.example` (create it if it doesn't exist)
   - Replace the placeholder values with your actual API key
   - ⚠️ Never commit your `.env` file to version control

Example `.env.example` file:
```env
# OpenWeather API Key - Get yours at https://openweathermap.org/api
OPENWEATHER_API_KEY=your_api_key_here
```

Your `.env` file should look like this (with your actual API key):
```env
OPENWEATHER_API_KEY=abc123def456...
```

## Development

Start the development server on `http://localhost:3000`:

```bash
# npm
npm run dev

# yarn
yarn dev

# pnpm
pnpm dev

# bun
bun run dev
```

## Building for Production

Build the application for production:

```bash
# npm
npm run build

# yarn
yarn build

# pnpm
pnpm build

# bun
bun run build
```

Preview the production build locally:

```bash
# npm
npm run preview

# yarn
yarn preview

# pnpm
pnpm preview

# bun
bun run preview
```

## Tech Stack

- [Nuxt 3](https://nuxt.com/) - The Vue Framework
- [TailwindCSS](https://tailwindcss.com/) - Utility-first CSS framework
- [OpenWeather API](https://openweathermap.org/api) - Weather data provider

## Security

- Never commit your `.env` file to version control
- Keep your API keys secure and private
- If you accidentally commit sensitive information, immediately rotate your API keys
- The `.env.example` file is provided as a template for required environment variables

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

## License

This project is open source and available under the [MIT License](LICENSE).

## Acknowledgments

- Weather icons from [Flaticon](https://www.flaticon.com/)
- Built with [Nuxt 3](https://nuxt.com/)
