## Steps to Containerize a .NET Application

1. Clone the Repository:

```bash
git clone https://github.com/saifaustcse/docker-node-nginx-starter
```

Navigate to the repository directory:

```bash
cd docker-node-nginx-starter
```

2. Build the Application Image

- Create a `Dockerfile` in the project directory, if it doesn't already exist.

3. Build the Docker image with a specific tag:

```bash
docker build -t docker-node-nginx-starter-v1 .
```

4. Run the Application in a Container using the built image:

```bash
docker run -d -p 127.0.0.1:4000:4000 --name docker-node-nginx-starter-container docker-node-nginx-starter-v1
```

5. Verify

- Open your browser and access the application at [http://localhost:4001](http://localhost:4001).
- List all running containers to verify that your application is running:

```bash
docker ps
```
