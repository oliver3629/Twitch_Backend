# Twitch Backend

Spring Boot backend for a Twitch discovery application. It uses the Twitch Helix API to search Twitch content, stores users and favorites in MySQL, and provides cached recommendations.

- [Twitch_Frontend](https://github.com/oliver3629/Twitch_Frontend)
- [AWS deployment guide](AWS_DEPLOYMENT.md)

## Requirements

- JDK 21
- Docker Desktop
- A Twitch application client ID and client secret

## Local setup

1. Start the local MySQL database:

   ```bash
   docker-compose up -d
   ```

   The provided configuration creates a `twitch` database at `localhost:3306` with username `root` and password `secret`.

2. Create a `.env` file in the backend project root, in the same folder as `build.gradle`:

   ```text
   twitch/
   ├── .env
   ├── build.gradle
   └── README.md
   ```

   Add your Twitch application credentials to `.env`:

   ```dotenv
   TWITCH_CLIENT_ID=your-client-id
   TWITCH_CLIENT_SECRET=your-client-secret
   ```

   The `.env` file is ignored by Git and must not be committed. Configure your IntelliJ run configuration to load this file because Spring Boot does not load a plain `.env` file automatically.

3. Open `src/main/java/com/laioffer/twitch/TwitchApplication.java` in IntelliJ. Click the green Run button beside `TwitchApplication`, then select **Run 'TwitchApplication'** to start the backend.

4. Open [http://localhost:8080](http://localhost:8080).

## Database configuration

To use a different MySQL database, set these environment variables before starting the application:

```text
DATABASE_URL=localhost
DATABASE_PORT=3306
DATABASE_USERNAME=root
DATABASE_PASSWORD=secret
DATABASE_INIT=always
```

`DATABASE_INIT=always` runs `database-init.sql` and recreates the tables whenever the application starts. After the first successful startup, use `DATABASE_INIT=never` if you want to preserve existing data.
