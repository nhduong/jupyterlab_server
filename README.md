# Setup a jupyterlab public server in Windows 10
Nguyen Hai Duong  
Chonnam National University  
  
    
## Environment
0. Windows 10 x64
1. Anaconda 4.2 with Python 3.5

## Environment Setup
1. Download and install [Anaconda 4.2.0 with Python 3.5](https://repo.continuum.io/archive/Anaconda3-4.2.0-Windows-x86_64.exe)
2. Open Command Prompt as Administrator
3. Type `conda install -c conda-forge jupyterlab` to install jupyterlab, then `jupyter serverextension enable --py jupyterlab` to enable jupyterlab. Validate the installation by `jupyter lab --version`
4. In order to protect jupyter server, we need to set the password by `jupyter notebook password`, enter the your password. The password will be saved in `C:\Users\<your name>\.jupyter\jupyter_notebook_config.json`
5. Open `jupyter_notebook_config.json`, add the following:
```
{
  "NotebookApp": {
    "password_required": true,
    "ip": "*",
    "password": <do not modify this line!>,
    "nbserver_extensions": {
      "jupyterlab": true
    },
    "notebook_dir": "path-to-your-project(e.g., D:\\jupyterlab)",
    "open_browser": false,
    "port": 8888,
	"certfile": "C:\\Users\\<your name>\\.jupyter\\jupyter_server.pem",
	"keyfile": "C:\\Users\\<your name>\\.jupyter\\jupyter_server.key",
	"allow_password_change": false
  }
}
```
6. Open `Task Scheduler`, `Create Basic Task...`, enter the task name, e.g., JupyterLab, select `When the computer starts`, `Start a program`, `C:\Program Files\Anaconda3\Scripts\jupyter-lab.exe`, `Open the Properties dialog....`, `Finish`, `Run whether user is logged on or not`, `Trigger`, `Delay task for 30 seconds`, `OK`
7. Click `Run` to start the server. Whenever the computer is restarted, the server will start automatically
8. Open Command Prompt as Administrator, type `Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux` to enable `Windows Subsystem for Linux` feature in Windows 10
9. Install `Ubuntu` for Windows from the `Windows Store`, run it
10. Enter `openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mykey.key -out mycert.pem` in the Ubuntu terminal to generate SSL certificate to sercure jupyter server
11. Open a web browser (not Internet Explorer!), go to https://<your computer public IP>:8888
12. You should receive some warnings from the browser, skip it
13. Enter the password to access you server
14. To logout the server, click `Help` > `Launch Classic Notebook` > `Logout`. This step is VERY important in case you used a public computer to access your server.