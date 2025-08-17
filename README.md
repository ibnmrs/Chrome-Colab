# Cloud-Based Browser with Hugging Face Uploader

This Google Colab notebook provides a cloud-based workflow to download files from complex websites and upload them directly to the Hugging Face Hub.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/ibnmrs/Chrome-Colab/blob/main/Chrome_Colab_2.ipynb)

---

## 🎯 Purpose & Motivation

This project solves a common problem: downloading files from websites that do not offer a direct download link. Standard tools like `wget` or `curl` fail on sites that require you to click a button, log in, or execute JavaScript to start a download.

The goal of this notebook is to provide a seamless **cloud-to-cloud workflow**:
1.  Use a full-featured Google Chrome browser within Colab to download any file, no matter how complex the site.
2.  Directly upload that file from the Colab instance to your Hugging Face Hub repository.

This method completely bypasses your local machine, saving your personal internet bandwidth and storage space. It's perfect for backing up models, datasets, or any large files you find online.

---

## ⚠️ Security Warning

While the Colab environment itself is secure, the browser session runs on a remote server. For your own security, **do not log into sensitive accounts**.

---

## 🚀 Key Features

-   **Interactive Chrome Browser**: Run a full desktop version of Google Chrome within Colab.
-   **User-Friendly Interface**: Access the browser through a clean Gradio web UI, embedded for convenience. No complex VNC client needed.
-   **Accessible Downloads**: A symbolic link is automatically created, making files downloaded in Chrome instantly visible in the Colab file explorer.
-   **Hugging Face Integration**: A dedicated section to log in and upload files/folders to the Hugging Face Hub.
-   **Flexible Uploads**: Supports uploading to model or dataset repositories, personal accounts or organizations, and public or private repos.

---

## 📖 How to Use

Follow the steps by running the cells in the notebook in order.

### Part 1: Running the Google Chrome Server

This section sets up and launches the browser environment.

1.  **Cell 1: Installation**
    -   Run this cell to install all necessary dependencies, including the virtual display server (`Xvfb`), window manager (`Fluxbox`), VNC server, Google Chrome, Gradio, and Cloudflare tunnel.

2.  **Cell 2: Run Google Chrome Server & Gradio**
    -   This is the main cell that starts all services.
    -   It launches the virtual desktop, starts Chrome, and creates a public Gradio URL for you to access it.
    -   Wait for the output to show `✅ EVERYTHING IS READY!`.
    -   Click the public Gradio link (ending in `.gradio.live` or `.trycloudflare.com`) to open the browser interface.
    -   If prompted for a VNC password, use `password`.

3.  **Cell 3: Link Downloads Folder**
    -   Run this cell to create a `Downloads` shortcut in the `/content/` directory. Any file you download using the Chrome browser will appear here, making it easy to access.

### Part 2: Uploading to Hugging Face Hub

This section allows you to upload files from your Colab session to the Hugging Face Hub.

1.  **Cell 4: Setup Environment**
    -   This cell installs the `huggingface_hub` library. It also provides an option to mount your Google Drive if needed.

2.  **Cell 5: Configure & Login to Hugging Face**
    -   **`huggingface_token`**: Get a `WRITE` access token from your [Hugging Face settings](https://huggingface.co/settings/tokens).
    -   **`model_repo_name` / `dataset_repo_name`**: Enter the name of the repository you want to upload to. The notebook will create it if it doesn't exist. You only need to provide one.
    -   **`organization_name`**: (Optional) If the repository belongs to an organization, enter its name here.
    -   **`make_private`**: Check this box if you want the created repository to be private.
    -   Run the cell to log in and prepare the repository.

3.  **Cell 6: Upload to Hugging Face**
    -   **`path_to_upload`**: Provide the full path to the file or folder in your Colab environment. **Example**: If you downloaded a file named `my_model.zip` using the browser, the path would be `/content/Downloads/my_model.zip`.
    -   **`path_in_repo`**: (Optional) Specify a folder or filename for the upload within the HF repository. If left blank, it will use the original name.
    -   **`commit_message`**: A descriptive message for your upload.
    -   Run the cell to start the upload. You will get a link to your file on the Hugging Face Hub upon completion.

---

## 💡 Example Workflow

1.  Run the **SERVER HUB** cells to launch the Chrome browser.
2.  Open the Gradio link and use Chrome to navigate to a website and download a large file (e.g., `data.zip`).
3.  The file automatically appears at `/content/Downloads/data.zip`.
4.  Run the **HUGGINGFACE HUB** cells, providing your token and a new dataset repository name.
5.  In the final upload cell, set `path_to_upload` to `/content/Downloads/data.zip`.
6.  Run the cell to upload your downloaded file directly to your new Hugging Face dataset repository.

---

## 🛠️ Requirements

The notebook handles all installations automatically. The core dependencies are:
-   `gradio`
-   `huggingface_hub`
-   `xvfb`, `fluxbox`, `x11vnc`
-   `cloudflared`
-   `google-chrome-stable`
