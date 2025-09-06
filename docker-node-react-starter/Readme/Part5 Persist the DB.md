### Persisting Data in Containers

#### Container's Filesystem

- Each container has its own isolated writable layer on top of shared image layers.
- Changes made in one container are not visible to another container, even if they use the same image.

#### Demonstration of Isolation

1. Start a container and create a file:

```bash
docker run --rm alpine touch greeting.txt
```

- Use `--rm` to automatically removes the container after the command completes.

2. Start another container and check for the file:

```bash
docker run --rm alpine stat greeting.txt
```

- The file does not exist because each container's writable layer is isolated.

#### Why Data Is Lost

- Containers start fresh from their image definition each time they are run.
- Changes made in a container are lost when the container is removed unless data is persisted using volumes.

#### Container Volumes

- Purpose: Volumes allow data to persist beyond the lifecycle of a container.
- Functionality:
- Changes in the container's mounted directory are reflected on the host.
- Volumes persist data across container restarts.

#### Types of Volumes

1. Volume Mounts:

- Managed by Docker.
- Referred to using a name.

2. Bind Mounts:

- Map a specific host directory to a container directory.
- Provides more control but is not commonly used for general cases.

#### Persisting Data for a To-Do App

- Default SQLite database path for the application: `/etc/todos/todo.db`.

1. Create a volume:

```bash
docker volume create todo-db
```

2. Start the container with the volume mounted:

```bash

docker build -t docker-node-react-starter-v2 .

# docker run -dp 127.0.0.1:3000:3000 docker-node-react-starter-v2
# docker run -dp 0.0.0.0:3000:3000 saifaustcse/docker-node-react-starter:v2

docker run -dp 127.0.0.1:3000:3000 --mount type=volume,src=todo-db,target=/etc/todos docker-node-react-starter-v2
docker run -dp 127.0.0.1:3000:3000 --mount type=volume,src=todo-db,target=/etc/todos saifaustcse/docker-node-react-starter:v2
```

- The `todo-db` volume is mounted to `/etc/todos` inside the container.

#### Verify Data Persistence

1. Add items to the app via the UI.
2. Stop and remove the container:

```bash
docker rm -f <container-id>
```

3. Restart the container with the same volume:

```bash
docker run -dp 127.0.0.1:3000:3000 --mount type=volume,src=todo-db,target=/etc/todos docker-node-react-starter-v2
```

- The previously added data will still be present.

#### Inspecting Volumes

- Locate where Docker stores the volume data:

```bash
docker volume inspect todo-db
```

- Example output:

```json
{
  "Mountpoint": "/var/lib/docker/volumes/todo-db/_data"
}
```

- The `Mountpoint` indicates the physical storage location of the volume on the host system (root access may be required to view it).

### SQLite shell access in Container

1. Access the Container:

```bash
docker exec -it <your-container-name> sh
```

2. Install SQLite (if not already installed):

```bash
apk add sqlite
```

Or for Debian-based images:

```bash
apt-get update
apt-get install -y sqlite3
```

3. Open the SQLite Database:

```bash
sqlite3 /etc/todos/todo.db
```

4. List Tables:

```sql
.tables
```

5. Query Data from a Table:

```sql
SELECT * FROM your_table_name;
```
