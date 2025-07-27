# Smart Multi-Camera Viewer

A modern, responsive web application for viewing multiple camera streams with real-time noise level monitoring.

## Features

- Real-time video streaming from RTSP/HLS sources
- Live noise level monitoring with visual feedback
- Light and dark theme support
- Responsive design that works on all devices
- Error boundaries and fallback UIs
- WebSocket-based real-time updates

## Tech Stack

- **Frontend**: React, video.js, WebSocket
- **Backend**: Python FastAPI, WebSockets
- **Styling**: Plain CSS with CSS Variables for theming

## Getting Started

### Prerequisites

- Node.js (v14 or later)
- Python 3.8 or later
- pip (Python package manager)

### Backend Setup

1. Navigate to the backend directory:
   ```bash
   cd backend
   ```

2. Create and activate a virtual environment (recommended):
   ```bash
   # On Windows
   python -m venv venv
   .\venv\Scripts\activate
   
   # On macOS/Linux
   python3 -m venv venv
   source venv/bin/activate
   ```

3. Install Python dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Start the backend server:
   ```bash
   uvicorn main:app --reload
   ```
   The backend will be available at `http://localhost:8000`

### Frontend Setup

1. Open a new terminal and navigate to the frontend directory:
   ```bash
   cd frontend
   ```

2. Install Node.js dependencies:
   ```bash
   npm install
   ```

3. Start the development server:
   ```bash
   npm start
   ```
   The frontend will be available at `http://localhost:3000`

## Project Structure

```
camera-viewer/
├── backend/
│   ├── main.py            # FastAPI application
│   └── requirements.txt    # Python dependencies
└── frontend/
    ├── public/             # Static files
    └── src/
        ├── components/     # React components
        │   ├── VideoPlayer.js
        │   ├── NoiseMeter.js
        │   └── ThemeToggle.js
        ├── context/        # React context
        │   └── ThemeContext.js
        ├── styles/         # CSS files
        │   └── App.css
        ├── App.js          # Main App component
        └── index.js        # Entry point
```

## Available Scripts

In the frontend directory, you can run:

- `npm start` - Start the development server
- `npm test` - Run tests
- `npm run build` - Build for production
- `npm run eject` - Eject from create-react-app

## Environment Variables

### Backend

Create a `.env` file in the backend directory with:

```
# Server configuration
HOST=0.0.0.0
PORT=8000

# CORS (comma-separated origins)
CORS_ORIGINS=*  # In production, replace with your frontend URL
```

## API Endpoints

- `GET /` - Health check
- `GET /api/stream` - Get stream information
- `WS /ws/noise` - WebSocket endpoint for real-time noise levels

## Deployment

### Backend

For production, use a production-ready ASGI server like Uvicorn with Gunicorn:

```bash
pip install gunicorn

# In production, you might want to use a process manager like systemd or supervisor
gunicorn -k uvicorn.workers.UvicornWorker -w 4 -b 0.0.0.0:8000 main:app
```

### Frontend

Build the production bundle:

```bash
cd frontend
npm run build
```

Serve the static files with a web server like Nginx or Apache.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
