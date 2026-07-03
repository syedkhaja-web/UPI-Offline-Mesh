# UPI Offline Mesh 

A Spring Boot backend that demonstrates offline UPI payments routed through a Bluetooth-style mesh network. This project simulates an environment with zero connectivity where a payment packet hops device-to-device until it reaches a node with internet access to sync with the backend.

## Features
- **Hybrid Encryption**: Uses RSA-OAEP + AES-GCM to securely encrypt payments so intermediaries cannot read or tamper with them.
- **Idempotency**: Prevents duplicate settlements if multiple bridge nodes upload the same packet simultaneously.
- **Replay Protection**: Verifies timestamps and nonces to ensure security against replay attacks.

## How to Run

### Prerequisites
- JDK 17 or newer

### Starting the Server (Windows)
Open a terminal in the project folder and run:
```cmd
.\mvnw.cmd spring-boot:run
```

Once the server has started, open your browser and navigate to:
**http://localhost:8080**

### Demo Flow
1. **Compose Payment**: Select a sender, receiver, and amount in the dashboard to inject an encrypted packet into the mesh.
2. **Gossip**: Run gossip rounds to simulate phones exchanging packets offline.
3. **Upload**: Flush the bridge nodes to simulate a device connecting to the internet and syncing all transactions with the backend ledger.

## Architecture
This is a standard Spring Boot 3 application using:
- Java 17
- Spring Web, Data JPA
- H2 In-Memory Database (for zero-setup demo execution)
- Thymeleaf (for the interactive frontend dashboard)

*Note: This is a demonstration environment. For a production deployment, the in-memory H2 database should be replaced with PostgreSQL/MySQL, and the in-memory cache should be replaced with Redis.*
