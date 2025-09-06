## Steps to Containerize a .NET Application

1. Clone the Repository:

```bash
git clone https://github.com/saifaustcse/docker-dotnet-starter
```

Navigate to the repository directory:

```bash
cd docker-dotnet-starter
```

2. Build the Application Image

- Create a `Dockerfile` in the project directory, if it doesn't already exist.

3. Build the Docker image with a specific tag:

```bash
docker build -t docker-dotnet-starter-v1 .
```

4. Run the Application in a Container using the built image:

```bash
docker run -d -p 8080:80 --name docker-dotnet-container docker-dotnet-starter-v1
```

5. Verify

- Open your browser and access the application at [http://localhost:8080](http://localhost:8080).
- List all running containers to verify that your application is running:

```bash
docker ps
```