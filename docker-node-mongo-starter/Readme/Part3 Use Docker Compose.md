## Start the Application with Docker Compose

1. Start MongoDB and Mongo-Express:

```bash
docker-compose -f docker-compose.yaml up
docker-compose -f docker-compose.yaml up --build -d
```

2. Open Mongo-Express in your browser: [http://127.0.0.1:5051](http://localhost:5051)

3. Create a `my-db` database and a `my-collection` collection, then insert a document with `{myid: 1, data: "some dynamic data loaded from db"}` using Mongo-Express.

4. Access your Node.js application UI from your browser: [http://127.0.0.1:3000](http://localhost:3000)

## Start the Application with Docker Compose and Environment Variables

1. Start MongoDB and Mongo-Express:

```bash
docker-compose -f docker-compose.yaml up --build -d
docker-compose -f docker-compose.yaml stop docker-node-mongo-starter-my-app
docker-compose -f docker-compose.yaml rm -f docker-node-mongo-starter-my-app
```

2. Rebuild the Application Image:

Rebuild your application container image. This ensures any updates to your app's code or `Dockerfile` are included in the image:

```bash
docker-compose -f docker-compose.yaml build -d my-app
export MONGO_DB_USERNAME=admin
export MONGO_DB_PWD=supersecret
```

3. Open Mongo-Express in your browser: [http://127.0.0.1:5051](http://localhost:5051)

4. Access your Node.js application UI from your browser: [http://127.0.0.1:3000](http://localhost:3000)
