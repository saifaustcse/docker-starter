
## Steps to Containerize a node.js Application

1. Clone the Repository:

```bash
git clone https://github.com/saifaustcse/docker-node-react-starter
```

Navigate to the repository directory:

```bash
cd docker-node-react-starter
```

2. Build the Application Image

- Create a `Dockerfile` in the project directory, if it doesn't already exist.

3. Build the Docker image with a specific tag:

```bash
docker build -t getting-started-v1 .
```

4. Run the Application in a Container using the built image:

```bash
docker run -d -p 127.0.0.1:3000:3000 getting-started-v1
```

5. Verify Running Containers

- Access the application in your browser at [http://localhost:3000](http://localhost:3000).
- List all running containers to verify that your application is running:

```bash
docker ps
```
