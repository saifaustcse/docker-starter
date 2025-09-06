## Steps to Containerize a .NET Application

1. Build the Application Image

- Create a `compose.yaml` in the project directory, if it doesn't already exist.

2. Run the application

- Navigate to the repository directory:

```bash
cd docker-dotnet-starter
```

- Inside the docker-dotnet-sample directory, run the following command in a terminal.

```bash
docker compose up --build.
docker compose up --build -d
```
- In the terminal, without background press ctrl+c to stop the application.

- Open your browser and access the application at [http://localhost:8080](http://localhost:8080).

3. Verify Running Containers

- List all running containers to verify that your application is running:

```bash
docker ps
```


In the terminal, run the following command to stop the application.

```bash
docker compose down
```
