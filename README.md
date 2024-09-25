# openwebui-demo

### How to Setting Up NVIDIA GPU support with windows WSL 2 and Docker on Ubuntu LTS

In this demo video (Bahasa): [Menjalankan ChatGPT secara lokal menggunakan docker openwebui dengan model phi3.5](https://youtu.be/o-A27OlPWcw)

```
System Specification
Processor  : 12th Gen Intel(R) Core(TM) i5-12450H
CPU cores  : 12 @ 2496.008 MHz
GPU        : NVIDIA GeForce RTX 3050 Laptop GPU, compute capability 8.6
AES-NI     : ✔ Enabled
VM-x/AMD-V : ✔ Enabled
RAM        : 7.6 GiB
Swap       : 2.0 GiB
Disk       : 2.0 TiB
Distro     : Ubuntu 24.04.1 LTS
Kernel     : 5.15.153.1-microsoft-standard-WSL2
VM Type    : WSL version: 2.2.4.0
Operating system: Windows 11 - 64 Bit
Docker Engine: Docker version 27.3.1, build ce12230 + Docker Compose version v2.29.2-desktop.2
```

If you have an NVIDIA GPU like me and want to leverage its power to enhance the performance of your ChatGPT model, follow these steps:

### Step 1: Install WSL 2 and Ubuntu LTS

1. Enable WSL: Open PowerShell as an administrator and run:

   ```powershell
   wsl --install
   ```

2. Set WSL 2 as Default:

   ```powershell
   wsl --set-default-version 2
   ```

3. Install Ubuntu LTS: You can find it in the Microsoft Store. Once installed, open it to complete the setup.

### Step 2: Install NVIDIA Drivers

1. Download and Install NVIDIA Drivers: Ensure you have the latest NVIDIA drivers that support WSL. You can download them from the [NVIDIA website](https://www.nvidia.com/Download/index.aspx).

2. Install CUDA Toolkit: Follow the instructions on the [CUDA Toolkit Installation Guide](https://docs.nvidia.com/cuda/wsl-user-guide/index.html#installation) to set it up within your WSL environment.

### Step 3: Install Docker in WSL 2

1. Install Docker: Follow these commands within your WSL terminal:

   ```bash
   sudo curl -sL https://get.docker.com
   ```

2. Start Docker:

   ```bash
   sudo service docker start
   ```

3. Add your user to the Docker group (to avoid using `sudo` with Docker):

   ```bash
   sudo usermod -aG docker $USER
   ```

   After running this command, log out and log back into your WSL terminal.

### Step 3: Install NVIDIA Container Toolkit

1. Set Up the NVIDIA Docker Toolkit:
   1.1 Configure the production repository:

    ```bash
      curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
        && curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
          sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
          sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
    ```

    1.2 Update the packages list from the repository and install Install the NVIDIA Container Toolkit packages

    ```bash
      sudo apt-get update
      sudo apt-get install -y nvidia-container-toolkit
    ```

   Follow the instructions from the [NVIDIA Docker documentation](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#docker) to install the NVIDIA Container Toolkit, which allows Docker to use your NVIDIA GPU.

2. Configure NVIDIA Docker Toolkit

   ```bash
    sudo nvidia-ctk runtime configure --runtime=docker
    sudo systemctl restart docker
   ```

3. Restart your system.

### Step 4: Run the Docker Container with GPU Support

Now, you can build and run your container, and it will utilize your NVIDIA GPU 💪

```bash
docker-compose up
```

### Step 5: Access OpenWebUI

Access the OpenWebUI as described in the previous steps, and you should now have a performance boost from your NVIDIA GPU.

### Please Note: For the first time you need create a local user by clicking up **sign up** inside Open WebUI 

## Benefits of Running ChatGPT Locally

1. Privacy: Keeping your data local means it’s not shared with third-party servers.
2. Control: You can modify and configure the model as needed.
3. Performance: Utilizing a GPU can significantly enhance performance, especially for larger models.

## Conclusion

Running ChatGPT locally using Docker OpenWebUI is a straightforward process that provides numerous benefits. With the optional setup for NVIDIA GPU support on WSL 2 and Ubuntu , you can take your local AI capabilities to the next level.

Feel free to dive into the configuration files and experiment with different settings to optimize your local environment 😁

---

### Additional Resources

- [Project Repository](https://github.com/taufiqpsumarna/openwebui-demo)
- [Docker Documentation](https://docs.docker.com/)
- [OpenWebUI GitHub Repository](https://github.com/open-webui/OpenWebUI)
- [Ollama Model](https://ollama.com/library)
- [NVIDIA Docker Documentation](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#docker)
- [WSL Installation Guide](https://docs.microsoft.com/en-us/windows/wsl/install)
