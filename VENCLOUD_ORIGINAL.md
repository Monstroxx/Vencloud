# Vencloud

Vencloud is Vencord's API for cloud settings sync!

## Self Hosting

> [!WARNING]
> Your instance has to be HTTPS capable due to [mixed content restrictions](https://developer.mozilla.org/en-US/docs/Web/Security/Mixed_content) in web browsers.

We provide a Docker build, so you don't need anything installed besides Docker!

### Using Docker and GitHub Container Registry

We publish a built, stable image on [GHCR](https://ghcr.io/vencord/vencloud). Pull the image using `ghcr.io/vencord/vencloud`. Use the
`docker-compose.yml` file we have in this repository as a reference for further setup!

### From Git

First of all, you'll have to clone the source code to a convenient location:
```sh
git clone https://github.com/Vencord/Vencloud
```

### Setting up the Config

Copy the example configuration (`.env.example`) to `.env`. Now open it with your text editor of trust and fill in the configuration values.
All variables are documented there!

### Running

Don't forget to direct your terminal to the Vencloud directory, e.g. via `cd Vencloud`!

#### Via Docker

1. Create a `docker-compose.override.yml` that maps the port from docker to your system.
   The following example assumes you will use port `8485`
   ```yaml
   services:
     backend:
       ports:
         - 8485:8080
   ```
2. Start the docker container via `docker compose up -d`. The server will be available at the configured host, in the above example `8485`

#### Natively

Please note that only the docker setup is supported by us.
The native instructions are only provided for advanced users and we can't provide support if you get stuck!
When in doubt, please use the docker setup.

Alongisde the Vencloud setup, you will also have to setup Redis. This will not be covered here, please refer to the Redis documentation.

1. Install the [Go programming language](https://go.dev/dl/)
2. Build the code: `go build -o backend`
3. Start the server:
   ```sh
   # Load the .env file
   export $(grep -v '^#' .env | xargs)

   ./backend
   ```
