# trivy-docker-image-scanner
This template uses Trivy to scan your image in your Docker Registry.

# Template Parameters
- **IMAGE_NAME:** The name of the image you want to scan.
- **IMAGE_VERSION_TAG:** The version/tag of the image you want to scan.
- **REGISTRY_USERNAME:** The username of your registry.
- **REGISTRY_PASSWORD:** The token of your registry.

## Examples
```yaml  
apiVersion: argoproj.io/v1alpha1
kind: Workflow
metadata:
  generateName: dag-test-
spec:
  entrypoint: dag-test
  templates:
    - name: dag-test
      dag:
        target: image-scanner
        tasks:
          - name: image-scanner-1
            templateRef:
              name: klovercloud-image-scanner
              template: trivy-docker-image-scanner
            arguments:
              parameters:
                - name: IMAGE_NAME
                  value: 'your-image-name'
                - name: IMAGE_VERSION_TAG
                  value: 'your-image-tag'
                - name: REGISTRY_USERNAME
                  value: 'your-registry-username'
                - name: REGISTRY_PASSWORD
                  value: 'your-registry-token'
```