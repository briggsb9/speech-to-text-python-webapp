# Speech-to-Text Python Web App

Sample for a simple speech-to-text Python web app for hosting on App Service.

This sample demonstrates how to create a web application that uses Azure's Speech Service to convert speech to text. The app is built using Flask and can be deployed on Azure App Service leveraging web sockets for real-time audio streaming.

## Setup Instructions

### 1. Create an Azure Speech Service

1. Go to the [Azure Portal](https://portal.azure.com/).
2. Create a new Speech Service resource.
3. Note down the `Subscription Key` and `Service Region`.

### 2. Quick deploy using Visual Studio Code

1. Install the [Azure App Service extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azureappservice) for Visual Studio Code.
2. Open your project in Visual Studio Code.
3. Sign in to your Azure account by clicking on the Azure icon in the Activity Bar and then clicking "Sign in to Azure".
4. Right-click on "App Service" in the Azure panel and select "Create New Web App...".
5. Follow the prompts to create a new web app:
   - Select your subscription.
   - Enter a globally unique name for your web app.
   - Select "Python 3.9" as the runtime stack.
   - Select "Linux" as the operating system.
6. Once the web app is created, right-click on it in the Azure panel and select "Deploy to Web App...".
7. Select your project folder when prompted.
8. Confirm the deployment when prompted.

### 3. Set Environment Variables

Set the following environment variables in your App Service's Application Settings:

1. In the Azure Portal, navigate to your App Service.
2. Under "Settings", select "Configuration".
3. Click on "New application setting" and add the following keys and values:
- `AZURE_SPEECH_KEY`: Your Azure Speech Service subscription key.
- `AZURE_SERVICE_REGION`: Your Azure Speech Service region.

### 4. Configure App Service

1. In the Azure Portal, navigate to your App Service.
2. Under "Settings", select "Configuration" and then "General settings".
4. Set the startup command in the app service general settings to:
   ```
   gunicorn --bind=0.0.0.0:8000 --worker-class=geventwebsocket.gunicorn.workers.GeventWebSocketWorker --timeout=600 app:app
   ```

### 6. Running Locally

To run the app locally, create a virtual environment and use the following command:
1. Create a virtual environment:
    ```bash
    python -m venv venv
    ```
2. Activate the virtual environment:

    Bash

    ```bash
    source venv/bin/activate
    ```

    Powershell

    ```powershell
    venv\Scripts\activate
    ```

2. Install the required packages:
    ```bash
    pip install -r requirements.txt
    ```

3. Set the environment variables in your local environment:

    Bash

    ```bash
    export AZURE_SPEECH_KEY=your_speech_key
    export AZURE_SERVICE_REGION=your_service_region
    ```

    Powershell

    ```Powershell
    $env:AZURE_SPEECH_KEY = "your_speech_key"
    $env:AZURE_SERVICE_REGION = "your_service_region"
    ```

4. Run the app:
    ```bash
    python app.py
    ```
5. Open your browser and navigate to `http://localhost:5000` to access the app.


### 7. Accessing the App

Once deployed, navigate to your App Service URL to access the speech-to-text web app.
