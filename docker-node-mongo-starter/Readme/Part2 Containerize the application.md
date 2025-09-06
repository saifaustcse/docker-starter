## Start the Application with Docker

1. Clone the Repository:

```bash
git clone https://github.com/saifaustcse/docker-node-mongo-starter
```

Navigate to the repository directory:

```bash
cd docker-node-mongo-starter
```

2. Create a Docker Network (Optional):

```bash
docker network create mongo-network
```

- If you skip this step, Docker will use the default network for communication.

3. Run the MongoDB container with authentication enabled:

- Without custom network:

```bash
docker run -d -p 127.0.0.1:27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password --name mongodb mongo
```

- With custom network:

```bash
docker run -d -p 127.0.0.1:27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password --name mongodb --net mongo-network mongo
```

4. Run the Mongo-Express container to visualize and manage MongoDB:

- Without custom network:

```bash
docker run -d -p 127.0.0.1:5051:8081 -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=password -e ME_CONFIG_MONGODB_SERVER=mongodb --name mongo-express mongo-express
```

- With custom network:

```bash
docker run -d -p 127.0.0.1:5051:8081 -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=password -e ME_CONFIG_MONGODB_SERVER=mongodb --net mongo-network --name mongo-express mongo-express
```

Note:

- Ensure the value of `ME_CONFIG_MONGODB_SERVER` matches the container name of the MongoDB instance (`mongodb` in this case).

5. Access Mongo-Express Logs (Optional):

```bash
docker logs mongo-express
```

You should see output similar to:

```
Mongo Express server listening at http://0.0.0.0:5051
Server is open to allow connections from anyone (0.0.0.0)
basicAuth credentials are "admin:pass", it is recommended you change this in your config.js!
```

6. Open Mongo-Express in your browser: [http://127.0.0.1:5051](http://127.0.0.1:5051) to access Mongo-Express.

7. Create a `my-db` database and a `my-collection` collection, then insert a document with `{myid: 1, data: "some dynamic data loaded from db"}` using Mongo-Express.

8. Create a Dockerfile (If Not Already Present).

9. Build the Docker Image for the app:

```bash
docker build -t docker-node-mongo-starter-v1 .
```

10. Run the Application using the built image:

```bash
docker run -d -p 127.0.0.1:3000:3000 --net mongo-network --name docker-node-mongo-container docker-node-mongo-starter-v1
export MONGO_DB_USERNAME=admin
export MONGO_DB_PWD=supersecret
```

11. Verify:

- Open your browser and access the application at [http://127.0.0.1:3000](http://127.0.0.1:3000).
- List all running containers to ensure everything is running:

```bash
docker ps
```

You should see the following containers:

- `mongodb`
- `mongo-express`
- `docker-node-mongo-container`
