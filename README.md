# Ollama Docker Project

This project provides two ways to run Ollama in Docker:

- **official/**: Uses the official Ollama Docker image
- **custom/**: Builds a custom image by downloading the Ollama binary

Below are instructions for using the official image with Docker Compose, as well as common Ollama tasks.

---

## Running Ollama (Official Image) with Docker Compose

1. **Navigate to the official folder:**
   ```sh
   cd official
   ```

2. **Start the container:**
   ```sh
   docker compose up -d
   ```
   This will pull the official Ollama image, start the service, and persist data in the `./data` folder.

3. **Stop the container:**
   ```sh
   docker compose down
   ```

4. **Enter the container's bash shell:**
   ```sh
   docker compose exec ollama bash
   ```
   This allows you to inspect files, debug, or run commands interactively inside the Ollama container.

**Note about `ollama serve` and port errors:**

If you try to run `ollama serve` inside the container and see an error like:

```
Error: listen tcp 0.0.0.0:11434: bind: address already in use
```

this means the Ollama server is already running (it starts by default when the container launches). You do not need to run `ollama serve` manually unless you have stopped the default process. You can still use other commands like `ollama list` or `ollama pull` inside the container.

---

## Common Ollama Tasks

Once the container is running, you can interact with Ollama using `docker compose exec` or `docker exec`:

### List Installed Models
```sh
docker compose exec ollama ollama list
```

### Pull a Model
```sh
docker compose exec ollama ollama pull deepseek-r1
```

### Check Available Models to Pull
Browse the model library at: [https://ollama.com/library](https://ollama.com/library)

### Run a Model (Chat)
```sh
docker compose exec -it ollama ollama run deepseek-r1
```

### Serve the API (default)
The container starts in `serve` mode by default and exposes port `11434`.
You can access the API at `http://localhost:11434`.

### Example: Using the API with curl
You can interact with the Ollama API using `curl`. For example, to generate a response from a model (e.g., `deepseek-r1`):

```sh
curl http://localhost:11434/api/generate \
  -d '{"model": "deepseek-r1", "prompt": "Why is the sky blue?"}'
```

Refer to the [Ollama API documentation](https://github.com/ollama/ollama/blob/main/docs/api.md) for more endpoints and usage examples.

---

## Notes
- The `custom/` folder works similarly, but builds the image from the included Dockerfile.
- Data is stored in the `data` folder inside each alternative.
- For more commands and options, see the [Ollama documentation](https://github.com/ollama/ollama) and [model library](https://ollama.com/library).
