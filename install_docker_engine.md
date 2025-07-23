# 📦 To install Docker Engine on your Ubuntu VM:
Run the following commands inside your Ubuntu VM:
```sudo apt-get update
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

### 🔍 What this does:
`sudo apt-get update`
- ➤ Updates the local list of available packages from all configured repositories.

`sudo apt-get install ...`

#### ➤ Installs required tools: 
| Package           | Purpose                                                                                         |
| ----------------- | ----------------------------------------------------------------------------------------------- |
| `ca-certificates` | Ensures secure HTTPS communication.                                                             |
| `curl`            | Command-line tool to fetch data from URLs (used to download Docker's GPG key).                  |
| `gnupg`           | Used to manage GPG keys (for verifying packages).                                               |
| `lsb-release`     | Provides Linux distribution info (like Ubuntu version name), needed to set up the correct repo. |




# Then add Docker’s official GPG key:
```sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

### 🔍 What this does:
`mkdir -p /etc/apt/keyrings`
- ➤ Creates a directory to store trusted GPG keys (if it doesn’t exist).

`curl -fsSL https://...`
- ➤ Downloads Docker's official GPG public key.

`gpg --dearmor -o ...`
- ➤ Converts the ASCII-armored GPG key into a binary format that APT can read and stores it in the keyrings directory.

- 🔐 This ensures packages from Docker can be verified as safe and authentic.

# Set up the repository:

```echo \
  "deb [arch=$(dpkg --print-architecture) \
  signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### 🔍 What this does:
Configures APT to use Docker's official package repository.

- Dynamically fills in:

- Your system's architecture (like amd64)

- Ubuntu version codename (like jammy, focal)

- Registers the repository in a safe and isolated file:
`/etc/apt/sources.list.d/docker.list`

# Install Docker Engine:
```sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
### 🔍 What this does:
Refreshes the package list again, now including Docker’s newly added repository.

# Then verify:

```sudo docker run hello-world
```

# Output for the above command

```vagrant@vagrant-ubuntu:~$ sudo docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
c9c5fd25a1bd: Pull complete 
Digest: sha256:ec153840d1e635ac434fab5e377081f17e0e15afab27beb3f726c3265039cfff
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (arm64v8)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

```
