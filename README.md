# NativeScript Vue WebSocket Example

This is a simple example project demonstrating WebSocket implementation in NativeScript Vue. The project shows how to establish WebSocket connections, send messages, and handle incoming messages in a NativeScript Vue application.

## Features

- WebSocket connection management
- Real-time message sending and receiving
- Clean and modern UI with NativeScript styling
- TypeScript support
- Echo server integration for testing

## Prerequisites

- Node.js
- NativeScript CLI
- Vue.js knowledge

## Installation

1. Clone the repository:
```bash
git clone git@github.com:NewbieScripterRepo/nativescript-websocket-example.git
cd nativescript-websocket-example
```

2. Install dependencies:
```bash
npm install
```

## Usage

1. Run the application:
```bash
ns run android
# or
ns run ios
```

2. The application will show a "Connect" button. Tap it to establish a WebSocket connection to the echo server.

3. Once connected, you can:
   - Type messages in the text field
   - Send messages using the "Send" button
   - View sent and received messages in the text area
   - Disconnect using the "Disconnect" button

## Code Structure

The main WebSocket functionality is implemented in `src/components/Home.vue`:

- `connect()`: Establishes WebSocket connection
- `sendMessage()`: Sends messages to the server
- `disconnect()`: Closes the WebSocket connection

## WebSocket Events

The example handles the following WebSocket events:
- `onopen`: Connection established
- `onmessage`: Message received
- `onerror`: Error handling

## Testing

This example uses the public WebSocket echo server (`wss://echo.websocket.org/`) for testing purposes. In a production environment, you should replace this with your own WebSocket server.

## Contributing

Feel free to submit issues and enhancement requests!

## License

[MIT License](LICENSE) 