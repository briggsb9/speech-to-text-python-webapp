# speech-to-text-python-webapp

Sample for a simple speech-to-text Python web app for hosting on App Service.

## Setup Instructions

### 1. Create an Azure Speech Service

1. Go to the [Azure Portal](https://portal.azure.com/).
2. Create a new Speech Service resource.
3. Note down the `Subscription Key` and `Service Region`.

### 2. Set Environment Variables

Set the following environment variables in your App Service's Application Settings:

- `AZURE_SPEECH_KEY`: Your Azure Speech Service subscription key.
- `AZURE_SERVICE_REGION`: Your Azure Speech Service region.

### 3. Configure App Service

1. Create a new Linux App Service.
2. Enable WebSockets (WebSockets are always enabled for Linux App Services).
3. Set the startup command to:
   ```
   gunicorn --bind=0.0.0.0:8000 --worker-class=geventwebsocket.gunicorn.workers.GeventWebSocketWorker --timeout=600 app:app
   ```

### 4. Quick deploy using Visual Studio Code

1. Install the [Azure App Service extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azureappservice) for Visual Studio Code.
2. Open your project in Visual Studio Code.
3. Sign in to your Azure account by clicking on the Azure icon in the Activity Bar and then clicking "Sign in to Azure".
4. Right-click on "App Service" in the Azure panel and select "Create New Web App...".
5. Follow the prompts to create a new web app:
   - Select your subscription.
   - Enter a globally unique name for your web app.
   - Select "Python 3.8" as the runtime stack.
   - Select "Linux" as the operating system.
6. Once the web app is created, right-click on it in the Azure panel and select "Deploy to Web App...".
7. Select your project folder when prompted.
8. Confirm the deployment when prompted.


### 6. Running Locally

To run the app locally, create a virtual environment and use the following command:
```
python app.py
```

### 7. Accessing the App

Once deployed, navigate to your App Service URL to access the speech-to-text web app.
