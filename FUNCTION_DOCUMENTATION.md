# Function and Component Documentation

This document provides a comprehensive overview of all the functions and components in the Smart Multi-Camera Viewer application.

## Backend (FastAPI)

### `main.py`

#### Classes

1. **ConnectionManager**
   - Manages WebSocket connections and broadcasts messages to all connected clients.
   - **Methods**:
     - `connect(websocket)`: Accepts a new WebSocket connection.
     - `disconnect(websocket)`: Removes a WebSocket connection.
     - `send_noise_level(noise_level)`: Sends noise level updates to all connected clients.

#### Functions

1. **websocket_endpoint(websocket)**
   - WebSocket endpoint that handles client connections for real-time noise level updates.
   - **Parameters**:
     - `websocket`: The WebSocket connection instance.

2. **simulate_noise_levels()**
   - Background task that generates random noise levels and broadcasts them to connected clients.

3. **get_stream_url()**
   - API endpoint that returns the stream URL and name.
   - **Returns**: JSON object with stream URL and name.

4. **root()**
   - Root endpoint that returns a simple status message.
   - **Returns**: JSON object with a welcome message.

5. **startup_event()**
   - FastAPI startup event that starts the noise level simulation.

## Frontend (React)

### Components

#### 1. `App.js`
   - Main application component that orchestrates all other components.
   - **State**:
     - `noiseLevel`: Current noise level in dB.
     - `streamUrl`: URL of the video stream.
     - `isConnected`: WebSocket connection status.
     - `ws`: WebSocket instance.
   - **Effects**:
     - Fetches the stream URL on component mount.
     - Manages WebSocket connection and message handling.

#### 2. `ThemeContext.js`
   - Context for managing the application theme (light/dark mode).
   - **Exports**:
     - `ThemeProvider`: Context provider component.
     - `useTheme`: Custom hook to access theme context.
   - **Theme Objects**:
     - `lightTheme`: Light theme color scheme and styles.
     - `darkTheme`: Dark theme color scheme and styles.

#### 3. `VideoPlayer.js`
   - Video player component that displays the video stream.
   - **Props**:
     - `streamUrl`: URL of the video stream.
     - `className`: Additional CSS class names.
   - **Features**:
     - Error boundary for graceful error handling.
     - Loading state while initializing.
     - Error state if stream fails to load.

#### 4. `NoiseMeter.js`
   - Displays the current noise level with a visual meter.
   - **Props**:
     - `noiseLevel`: Current noise level in dB.
   - **Features**:
     - Visual meter that changes color based on noise level.
     - Helpful text describing the noise level.

#### 5. `ThemeToggle.js`
   - Button to toggle between light and dark themes.
   - **Features**:
     - Updates theme in context and localStorage.
     - Displays appropriate icon based on current theme.

### Utility Functions

1. **calculateFillPercentage(level)**
   - Calculates the fill percentage for the noise meter.
   - **Parameters**:
     - `level`: Current noise level in dB.
   - **Returns**: Fill percentage (0-100).

2. **getNoiseColor(level)**
   - Determines the color of the noise meter based on the noise level.
   - **Parameters**:
     - `level`: Current noise level in dB.
   - **Returns**: Color code.

## Styling

### `App.css`
   - Contains all the styling for the application.
   - Uses CSS variables for theming.
   - Implements responsive design with media queries.
   - Includes animations and transitions for better UX.

## Data Flow

1. The backend generates random noise levels every 2 seconds and broadcasts them via WebSocket.
2. The frontend connects to the WebSocket and updates the UI in real-time.
3. The video player displays the stream from the provided URL.
4. The theme toggle updates the application theme, which is persisted in localStorage.

## Error Handling

- **Video Player**: Includes error boundary and fallback UI.
- **WebSocket**: Handles connection errors and reconnection logic.
- **API Calls**: Includes error handling for failed requests.

## Performance Considerations

- Uses React.memo for performance optimization.
- Implements proper cleanup in useEffect hooks.
- Uses CSS variables for efficient theming.
- Lazy loading for components if the application grows.

## Security Considerations

- CORS is configured to allow requests from any origin in development.
- In production, configure CORS to allow only trusted domains.
- Sensitive configuration should be stored in environment variables.
