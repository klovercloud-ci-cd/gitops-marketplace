# basic-deployment-trigger

This template automates the deployment process on an Argo CD server. It works in two steps:

1.  **Trigger Deployment:**

- Sends a PUT request to a specified URL.
- This triggers the deployment process on the Argo CD server.
2.  **Monitor Deployment Status:**

- Sends a GET request to another specified URL.
- Receives a response indicating the current deployment status:
  -   **SUCCEEDED:** Template is considered successful.
  -   **FAILED:** Template is considered a failure.
  -   **RUNNING:** Deployment is ongoing.


## Template Parameters

- **PUT_REQUEST_URL:** Sends a PUT request to the given url to initiate the deployment.
- **GET_REQUEST_URL:** Sends GET request to monitor the Deployment Status until it is successfully deployed or fails to deploy.

## Examples
```yaml  
apiVersion: argoproj.io/v1alpha1
kind: Workflow
metadata:
  generateName: deployment-trigger-example-
spec:
  entrypoint: deployment-trigger-example
  templates:
    - name: deployment-trigger-example
      dag:
        tasks:
          - name: deployment-trigger-example
            templateRef:
              name: klovercloud-deployment-trigger
              template: basic-deployment-trigger
            arguments:
              parameters:
                - name: PUT_REQUEST_URL
                  value: ''
                - name: GET_REQUEST_URL
                  value: ''
```