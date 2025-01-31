# Deployment

This folder contains the resources required for deploying the trained model onto Highwind.

## Usage

> All commands below are run from this directory.

### Building your model image

This step builds the Kserve predictor image that contains your model.
The saved_model is copied to the deployments folder. This was done using the cp command on  bash
    ```
1. Build the container locally and give it a tag

    ```bash
    docker build -t local/highwind-examples/dyu-fr-inference:latest .
    ```

### Local testing

1. After building the Kserve predictor image that contains the model, spin it up to test the model inference

    ```bash
    docker compose up -d
    docker compose logs
    ```

1. Finally, send a payload to the model to test its response. A `POST` request with an example JSON payload was used to test the response.
    ```

    Windows PowerShell

    ```PowerShell
    $json = Get-Content -Raw -Path ./input.json
    $response = Invoke-WebRequest -Uri http://localhost:8080/v2/models/model/infer -Method Post -ContentType 'application/json' -Body ([System.Text.Encoding]::UTF8.GetBytes($json))
    $responseObject = $response.Content | ConvertFrom-Json
    $responseObject | ConvertTo-Json -Depth 10
    ```
