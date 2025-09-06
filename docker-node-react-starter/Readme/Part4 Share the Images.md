### Sharing the Images

1. Create a Docker Hub Account

- Docker Hub is the default registry for sharing Docker images.
- Sign up or log in to [Docker Hub](https://hub.docker.com).
- Create a public repository named `docker-node-react-starter`.

2. Log in to Docker Hub:

```bash
docker login -u saifaustcse
```

3. Tag the image with your Docker ID:

```bash
docker tag getting-started-v1 saifaustcse/docker-node-react-starter
docker tag getting-started-v1 saifaustcse/docker-node-react-starter:v1
```

4. Run the the Container from new image

```bash
docker run -dp 127.0.0.1:3000:3000 saifaustcse/docker-node-react-starter
docker run -dp 127.0.0.1:3000:3000 saifaustcse/docker-node-react-starter:v1
```

5. Push the image to Docker Hub:

```bash
docker push saifaustcse/docker-node-react-starter
docker push saifaustcse/docker-node-react-starter:v1
```

### Run the Image on a New Instance

- Use [Play with Docker](https://labs.play-with-docker.com/)
- Select Login and then select docker from the drop-down list.
- Sign in with your Docker Hub account and then select Start.
- Log in to Play with Docker using doc and start a new instance.
- Select the ADD NEW INSTANCE option on the left side bar. If you don't see it, make your browser a little wider. After a few seconds, a terminal window opens in your browser.

1. Pull and run the image:

```bash
docker run -dp 127.0.0.1:3000:3000 saifaustcse/docker-node-react-starter
docker run -dp 0.0.0.0:3000:3000 saifaustcse/docker-node-react-starter:v1
```

Port Binding

- `127.0.0.1`: Limits port access to the host's loopback interface.
- `0.0.0.0`: Exposes ports on all host interfaces, making them accessible externally.

Publishing Ports

- Use `--publish` (`-p`) to expose container ports; otherwise, ports remain inaccessible externally on bridge networks.
- `-p 8080:80`: Maps host port 8080 to container port 80 (TCP).
- `-p 192.168.1.100:8080:80`: Maps host IP-specific port 8080 to container port 80.
- `-p 8080:80/udp`: Maps host port 8080 to container port 80 (UDP).
- `-p 8080:80/tcp -p 8080:80/udp`: Maps both TCP and UDP ports.

2. Multi-Platform Compatibility (Optional)

- For `amd64` compatibility (e.g., Play with Docker):

```bash
docker build --platform linux/amd64 -t saifaustcse/docker-node-react-starter .
docker build --platform linux/amd64 -t saifaustcse/docker-node-react-starter:v1 .
```

3. Access the Application

- Open the app in your browser via the instance's 3000 badge or manually open the port.
