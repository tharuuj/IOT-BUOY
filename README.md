# IoT Buoy Realtime Dashboard

Full React + TypeScript dashboard for environmental monitoring with Firebase Realtime Database.

## Features

- Multi-page analytics dashboard
- Layered model support: Raw -> Silver -> Gold
- Realtime stream integration from Firebase Realtime Database
- Overview KPIs + WQI gauge + map panel
- Realtime timeline + gauges + buoy motion + live alerts
- IoT device health and sensor reliability visualizations
- Environmental correlation and relationship analytics
- Forecasting and bleaching risk indicator
- Historical explorer with filters

## Dashboard Pages

1. Overview
2. Real-Time Monitoring
3. IoT Device Health
4. Environmental Analytics
5. Forecasting
6. Historical Data Explorer
7. Alerts

## Tech Stack

- React 19
- TypeScript
- Vite
- React Router
- Recharts
- Framer Motion
- Firebase Web SDK (Realtime Database)

## Project Structure

```
src/
  components/
  data/
  hooks/
  layout/
  lib/
  pages/
  types/
  utils/
```

## Firebase Setup

1. Copy `.env.example` to `.env`.
2. Fill in your Firebase web config values.
3. Ensure your Realtime Database has secure auth-based rules.
4. Provide dashboard data under the root path `dashboard`.

The app reads from:

`dashboard`

Expected shape:

```json
{
  "dashboard": {
    "raw": {
      "temperature": [{ "timestamp": 0, "value": 0 }],
      "ph": [{ "timestamp": 0, "value": 0 }],
      "turbidity": [{ "timestamp": 0, "value": 0 }],
      "light": [{ "timestamp": 0, "value": 0 }],
      "gyro": [{ "timestamp": 0, "x": 0, "y": 0, "z": 0 }]
    },
    "silver": {
      "environmentalReadings": [
        { "timestamp": 0, "temperature": 0, "ph": 0, "turbidity": 0, "light": 0 }
      ]
    },
    "gold": {
      "waterQualityAndBleachingRisk": [
        { "timestamp": 0, "waterQualityIndex": 0, "bleachingRisk": "low", "riskScore": 0 }
      ],
      "alerts": [
        {
          "id": "a1",
          "timestamp": 0,
          "severity": "high",
          "message": "sample",
          "sensor": "temperature",
          "acknowledged": false
        }
      ],
      "dailySummary": [
        {
          "date": "2026-03-14",
          "avgTemperature": 0,
          "avgPh": 0,
          "avgTurbidity": 0,
          "avgLight": 0,
          "avgWqi": 0
        }
      ],
      "deviceStability": [
        { "timestamp": 0, "stabilityScore": 0, "movementIntensity": 0 }
      ],
      "forecast": [
        { "timestamp": 0, "historical": 0, "predicted": 0, "lower": 0, "upper": 0 }
      ]
    },
    "deviceStatus": {
      "online": true,
      "signalStrength": 80,
      "battery": 70,
      "solarCharging": true,
      "lastSeen": 0
    }
  }
}
```

If Firebase is not configured or no `dashboard` node exists, the app automatically uses realistic mock data for UI preview.

## Run

```bash
npm install
npm run dev
```

## Build

```bash
npm run build
npm run preview
```

## Security Notes

- Do not use deprecated Database Secrets.
- Do not expose Firebase Admin service keys in frontend code.
- Keep Admin SDK on server-side only (Cloud Functions / backend service).
- Use Firebase Authentication + role-based access and strict database rules.
