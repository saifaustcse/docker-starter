### Updating the Application

1. Update the Source Code

- Modify the placeholder text in `src/static/js/app.js` at line 56:

```diff
- <p className="text-center">No items yet! Add one above!</p>
+ <p className="text-center">Version 1</p>
```

2. Rebuild the Docker image again with the updated code:

```bash
docker build -t getting-started-v1 .
```

3. Handle Port Conflict Errors

- If the previous container is still running, stop and remove it:

```bash
docker ps                    # List running containers
docker stop <container-id>   # Stop the container
docker rm <container-id>     # Remove the container
```

- Alternatively, stop and remove the container in one step:

```bash
docker rm -f <container-id>
```

4. Run the Updated Container

```bash
docker run -dp 127.0.0.1:3000:3000 getting-started-v1
```

5. Verify the Update

- Refresh [http://localhost:3000](http://localhost:3000) to see the updated text

## Remove Image

1. Check Images Before Deletion:

```bash
docker images
```

2. Remove a Specific Image by Image ID or Name

```bash
docker rmi <image-id>  # By image ID
docker rmi <image-name>  # By image name
```

3. Remove Multiple Images

```bash
docker rmi <image-id-1> <image-id-2> ...
```

4. Remove All Dangling (Unused) Images

- These are images that are not tagged and not associated with any container.

```bash
docker image prune
```

5. Force Remove an Image

- Use the `-f` flag to forcefully remove an image, even if it is in use by stopped containers.

```bash
docker rmi -f <image-id>
```

6. Remove All Images

- Removes all images on your system (be cautious as this action cannot be undone):

```bash
docker rmi $(docker images -q)
```
