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



