# trivy-quay-image-scanner
This template uses Trivy to scan your image in your Quay Registry.

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
          - name: image-scanner
        templateRef:
          name: klovercloud-image-scanner
          template: trivy-quay-image-scanner
        arguments:
          parameters:
            - name: IMAGE_NAME
              value: 'potato-v1-dev-branch'
            - name: IMAGE_TAG
              value: '87c1eb28e69f4a80a542'
            - name: REGISTRY_USERNAME
              value: 'rafsnil'
            - name: REGISTRY_PASSWORD
              value: 'hehehehehehehehehehehehehehehehehehehehehehehehehehehehehehe'
```