# ITE183 Laboratory 2 — HTTP and WebSocket

A small HTTP server and real-time, multi-client chat application built with **Bonezegei Scripting Language (BZG)**. The server delivers the chat page over HTTP and uses WebSocket events to receive and broadcast messages.

## Requirements

- Bonezegei Scripting Language **v1.3.3**, as specified for this laboratory
- A desktop browser with WebSocket support
- A terminal or command prompt

## Project structure

```text
ITE183_Lab2_Websocket/
├── app.bzg
├── package.json
├── .gitattributes
├── public/
│   ├── index.html
│   └── 404.html
├── lib/                 # Installed dependency files
└── README.md
```

The `lib/` directory is provided by the dependency installation step; do not create a replacement for the HTTP library by hand.

## Installation

1. Install Bonezegei v1.3.3.
2. Open a terminal in the project directory.
3. Install the project dependency:

   ```bash
   bzg install
   ```

## Run the server

Start the application:

```bash
bzg run
```

The server listens on port **8000**. Keep the terminal open while testing.

## Test the application

1. Open [http://localhost:8000/](http://localhost:8000/) in a browser.
2. Wait for the status to show **Connected**.
3. Open the same address in a second browser tab or window.
4. Send a message from either tab. The server broadcasts it to all connected clients.
5. Check the terminal for connection, received-message, and disconnection logs.
6. Visit [http://localhost:8000/anything](http://localhost:8000/anything) to view the custom not-found page.

## How it works

- `include("lib/http.bzg")` loads the HTTP/WebSocket library installed for the project.
- `http(8000)` creates the server on port 8000.
- `server.get` serves `public/index.html` at `/` and `public/404.html` for other paths.
- `server.onConnect` runs when a WebSocket client connects and sends that client a welcome message with `server.send()`.
- `server.onData` receives a message and uses `server.sendAll()` to broadcast it to connected clients.
- `server.onDisconnect` logs when a client leaves.
- The browser connects to `ws://localhost:8000`, sends messages through the WebSocket, and displays incoming messages.

## Notes

- This is a local laboratory demonstration. The WebSocket address is intentionally `ws://localhost:8000`; it is not configured for public deployment or TLS.
- If port 8000 is already in use, stop the other process before starting this server.
- If the browser cannot connect, confirm that the Bonezegei server is running and that the dependency installation completed successfully.

## License

This project is released under the MIT License. See [LICENSE](LICENSE).
