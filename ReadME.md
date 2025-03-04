# Introduction
This is a FastAPI backend service for real-time speech recognition and summarization.

The main goal of the project is to transcribe consultations in real-time and provide detailed summarization automatically after consultations end.

By leveraging natural language processing and machine learning, it can transcribe consultations in real-time with 0.1 seconds delay, 98-99% accuracy, extract key information, and automatically generate structured summarization.

# Main Functionalities

1. Real time transcription using FasterWhisper(https://github.com/SYSTRAN/faster-whisper), latency of 0.1 seconds, and 98-99% accurate.

2. Prvoide sturctured summarization with all the key details using LLaMA3 model.

# How to Run Server with Docker

## Prerequsites

1. You should have GPU server to run server.

   You can follow `docs/GPU-Server-Setup-Guides.md` file to setup GPU server on AWS.

2. Your instance should have installed docker runtime.

   You can verify if docker is installed on your computer `docker --version`.
   If it's not working, please follow this link to install
   Docker: https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository

3. Your instance should have installed NVIDIA driver compatible with your GPU server.

   To check if NVIDIA driver is installed, you can run `nvidia-smi`.
   If it's not working, you can follow below commands to install driver(ubuntu 22.04).

    ```

    1. wget https://developer.download.nvidia.com/compute/cuda/12.4.1/local_installers/cuda_12.4.1_550.54.15_linux.run

    2. sudo sh cuda_12.4.1_550.54.15_linux.run

    3. sudo reboot
    
    ```

4. You should have installed nvidia container toolkit so that docker containers can access GPUs on host computer.

   Follow these commands to install nvidia container toolkit.

    ```
    1. curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
    && curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
        sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
        sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list

    
    2. sudo apt-get update

    3. sudo apt-get install -y nvidia-container-toolkit

    4. sudo systemctl restart docker (Restart Docker)

    ```

5. Install make and docker compose

Follow this guide: https://docs.docker.com/engine/install/ubuntu/

6. Add your user to docker group

    ```
    sudo usermod -aG docker $USER
    ```

   You should logout and login again to apply changes.

## Running Backend Server

1. Clone the repository.

2. Copy ```.env.example``` file and rename it as ```.env```
   
   Set your environment variables there.

3. Run ```make docker-build``` to build docker images.

4. Run ```make docker-up``` to compose up docker containers.

   Now, Your server will be available at 8000 port.

