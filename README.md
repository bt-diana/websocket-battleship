# WebSocket Battleship Server

This project is a **backend for a Battleship game** using **WebSocket**. It allows players to create and join game rooms, place ships, and play the classic Battleship game in real-time. The backend is built using **Node.js** and **WebSocket** library (`ws`).

## Features

### WebSocket Server
- Starts a WebSocket server that listens for player connections.
- Handles player registration, game room management, ship placement, and gameplay actions.
- Provides support for real-time communication between players during the game.
- Properly closes WebSocket connections when the game ends.

### Game Logic
- Players can:
  - Register/login with a username and password.
  - Create or join a game room.
  - Place ships on the game board.
  - Attack opponent's ships.
  - Receive updates about game status and shot results.
  - See the list of rooms and current players.
  - View the leaderboard with the latest winners.

### Load Balancing
- Uses the **Cluster API** to distribute WebSocket connections across multiple instances.
- Implements a **Round-robin algorithm** for fair load distribution.

### Single-Player Mode
- Supports playing against a simple AI bot.

## Installation

1. Clone the repository:

```bash
git clone <repository-link>
```

2. Navigate to the project directory:

```bash
cd websocket-battleship
```

3. Install dependencies:

```bash
npm install
```

4. Create a .env file in the root directory and specify the port:

```ini
PORT=8181
```

## Running the Project
### Development Mode
Start the server with automatic reload:

```bash
npm run start:dev
```

### Production Mode
Build and run the server:

```bash
npm run start
```

### Multi-Instance Mode
Start multiple instances with load balancing:

```bash
npm run start:multi
```

The server will listen on the following ports:

- Main WebSocket Server: ws://localhost:8181

- WebSocket connections via load balancer:

    - ws://localhost:8182

    - ws://localhost:8183

    - ws://localhost:8184

## Game Flow
1. Player Registration:

Players register or log in with a username and password.

2. Room Creation and Joining:

Players can create a new game room or join an existing one.

3. Ship Placement:

Players place ships on their game boards.

4. Game Start:

The game starts when both players have joined and placed their ships.

5. Gameplay:

Players take turns attacking each other's ships.

The game continues until one player sinks all of the opponent's ships.

6. Victory:

The server announces the winner and updates the leaderboard.

## Player Commands
- Register/Login:

```ts
{
  type: "reg",
  data: {
    name: "playerName",
    password: "playerPass"
  },
  id: 0
}
```

- Create Room:

```ts
{
  type: "create_room",
  data: "",
  id: 0
}
```

- Join Room:

```ts
{
  type: "add_user_to_room",
  data: {
    indexRoom: 1
  },
  id: 0
}
```

- Place Ships:

```ts
{
  type: "add_ships",
  data: {
    gameId: 1,
    ships: [
      {
        position: { x: 2, y: 3 },
        direction: true,
        length: 3,
        type: "medium"
      }
    ],
    indexPlayer: 1
  },
  id: 0
}
```

- Attack:

```ts
{
  type: "attack",
  data: {
    gameId: 1,
    x: 5,
    y: 7,
    indexPlayer: 1
  },
  id: 0
}
```

- Random Attack:

```ts
{
  type: "randomAttack",
  data: {
    gameId: 1,
    indexPlayer: 1
  },
  id: 0
}
```

## Technologies Used

- **Node.js** (v22.14.0 or higher)
- **WebSocket (ws)**
- **TypeScript** (optional)
- **Nodemon**, **ts-node-dev** (for development)
- **Cluster API** (for load balancing)
- **Prettier**, **ESLint** (code quality)
- **Jest** (for testing)

## Testing

Run automated tests:

```bash
npm test
```

## Example Test Scenario

1. **Register two players.**

2. **Create a game room.**

3. **Join the second player to the room.**

4. **Start the game and place ships.**

5. **Execute some attack commands.**

6. **Check the winner announcement.**

---

## License

This project is licensed under the [MIT License]().
