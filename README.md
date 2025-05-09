# Jupyter Docker Image

*Navigation*:

1. [How to install Jupyter?](#how-to-install-jupyter)
2. [How to stop / uninstall Jupyter?](#how-to-stop--uninstall-jupyter)
3. [How to run code in Jupyter?](#how-to-run-code-in-jupyter)

---

> ⚠️ Important note ⚠️
> 
> The purpose of this Jupyter Docker image is to make sure everyone has the identical working environment, i.e., Python and its packages' versions to be the same for everyone. This avoid the issue that the code can run on my device but not yours.

![image](https://github.com/user-attachments/assets/bd40b7b6-941c-429f-a160-0dd0eae0d295)

## How to install Jupyter?

Before installing Jupyter, ensure that Docker is installed on your system. For optimal performance, it is recommended to have at least 16 GB of RAM, an NVIDIA GPU with CUDA support and a minimum of 4 GB of GPU memory, and at least 20 GB space available on disk.

### Step 1: Download Jupyter configuration files

Choosing a preferred directory.

- For Windows, run the following command in Windows command prompt.

  ```bash
  powershell -Command "Invoke-WebRequest -Uri 'https://firescape.project.gd.edu.kg/assets/zip/jupyter.zip' -OutFile 'jupyter.zip'; Expand-Archive -Path 'jupyter.zip' -DestinationPath .; Rename-Item 'FireScape-jupyter' 'firescape_jupyter'; Remove-Item 'jupyter.zip'"
  ```

- For Linux / MacOS, run the following command in terminal. Make sure you have already installed `curl` and `unzip`.

  ```bash
  curl -L -o jupyter.zip https://firescape.project.gd.edu.kg/assets/zip/jupyter.zip && unzip jupyter.zip && mv FireScape-jupyter firescape_jupyter && rm jupyter.zip
  ```

### Step 2: Switch the directory

Run the following command.

```bash
cd firescape_jupyter
```

### Step 3: Build the Docker image

Run the following command to build the Docker image. Make sure you have already installed Docker. This process is time consuming. Make sure your have a stable internet connection.

```bash
docker build --no-cache -t firescape_jupyter .
```

### Step 4: Run the Docker container

- For Windows, run one of the following commands in Windows command prompt.

  - (Recommended) Run with GPU in addition to CPU.

    ```bash
    docker run -d --name firescape_container -p 8888:8888 --gpus all -v "%cd%\working:/app/working" firescape_jupyter
    ```

  - Run with CPU only.

    ```bash
    docker run -d --name firescape_container -p 8888:8888 -v "%cd%\working:/app/working" firescape_jupyter
    ```

- For Linux / MacOS, run the following command in terminal.

  - (Recommended) Run with GPU in addition to CPU.

    ```bash
    docker run -d --name firescape_container -p 8888:8888 --gpus all -v "$(pwd)/working:/app/working" firescape_jupyter
    ```

  - Run with CPU only.

    ```bash
    docker run -d --name firescape_container -p 8888:8888 -v "$(pwd)/working:/app/working" firescape_jupyter
    ```

### Step 5: Start Jupyter

Open your browser, type http://127.0.0.1:8888 to access the Jupyter Lab interface.

## How to stop / uninstall Jupyter?

### Stop and Remove the Docker Container

- To stop the Docker container, run the following command.

  ```bash
  docker stop firescape_container
  ```

- To remove the Docker container, run the following command.
  
  ```bash
  docker rm firescape_container
  ```

### Uninstall the Docker Image

To remove the Docker image, run the following command.

```bash
docker rmi firescape_jupyter
```

## How to Run Code in Jupyter

To run code in Jupyter, follow the steps below:

### 1. Prepare Your Local Directory
- Place all your configuration files for Jupyter in your local directory.
- The contents inside the `working/` folder will be synchronized with this directory, so ensure it reflects the latest state.

### 2. Check Dependencies
- All necessary dependencies are already included in Jupyter.
- You don't need to manually install them, making it easy to get started right away.
- In case if you need additional dipendencies, modify the `requirements.txt` in the configuration files in your local machine, then rebuild the Docker image and container, or simply using `!pip install`.

### 3. Create a New Notebook or Script
- You can create a new Jupyter notebook or a Python script to write your code.
- Ensure your notebook or script is placed inside the `working/` folder to enable synchronization.

### 4. Explore Example Notebooks
- If you're new to Jupyter or want to quickly see how things work, check out the example notebook at `working/script/example.ipynb`.
- These examples will help you understand how to use the system.

### 5. Run Your Code
- Once your notebook or script is ready, simply run it.
- Any outputs or changes made within the `working/` directory will be reflected in your local directory.
