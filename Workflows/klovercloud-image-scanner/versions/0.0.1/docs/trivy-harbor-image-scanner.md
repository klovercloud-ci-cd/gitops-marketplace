# trivy-harbor-image-scanner
This template uses Trivy to scan your image in your Harbor Registry.

# Template Parameters
- **HARBOR_REGISTRY_URL:** The server url of your registry.
- **PROJECT_NAME:** The project name of your registry.
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
              template: trivy-harbor-image-scanner
            arguments:
              parameters:
                - name: IMAGE_NAME
                  value: 'potato-v1-dev-branch'
                - name: IMAGE_VERSION_TAG
                  value: '87c1eb28e69f4a80a542'
                - name: REGISTRY_USERNAME
                  value: 'rafsnil'
                - name: REGISTRY_PASSWORD
                  value: 'hehehehehehehehehehehehehehehehehehehehe'
                - name: HARBOR_REGISTRY_URL
                  value: 'harbor.klovercloud.io'
                - name: PROJECT_NAME
                  value: 'test'
```