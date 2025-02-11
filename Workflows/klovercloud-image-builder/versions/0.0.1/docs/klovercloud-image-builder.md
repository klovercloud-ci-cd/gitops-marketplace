# klovercloud-image-builder
This template is a DAG template which consists of three steps:

1.  **Secret Creation:** Creates a Secret in your Kubernetes Cluster
2.  **Image Build:** Creates a Kaniko Pod which is responsible for building your image from your given repository and push it to your given registry
3. **Resource Clean up:** After the success/failure of your Kaniko Pod, the Kaniko Pod is then deleted from your cluster


# Template Parameters

- **SECRET_NAME:** The name of Secret which will be created in your Kubernetes Cluster. 
- **REGISTRY_DOCKER_CONFIG_JSON_VALUE:** The .dockerconigjson value of your Secret.
- **GIT_USERNAME:** The username of your Git account.
- **GIT_TOKEN:** The token of your Git account.
- **GIT_REPOSITORY_URL_WITHOUT_HTTPS:** The https clone url of your repository without the "https".
- **GIT_REPOSITORY_BRANCH:** The repository for which you want the image to be built.
- **REGISTRY_PREFIX:** This is the prefix before your repository, e.g. for docker there's no prefix, for harbor 'habor_server_url/project_name/' and for quay 'quay.io/'. NOTE: If there's a prefix, always give the last forward slash '/'.
- **REGISTRY_USERNAME:** The name of your registry username.
- **IMAGE_NAME:** The name of the new image.
- **IMAGE_VERSION_TAG:** The image tag of the new image.
- **PATH_TO_DOCKERFILE:** The location of the Dockerfile in your repository, e.g. ("Dockerfile" means in root directory or "some-directory/Dockerfile")

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
        tasks:
          - name: image-builder
            templateRef:
              name: klovercloud-private-repo-private-registry-image-builder
              template: klovercloud-image-builder
            arguments:
              parameters:
                - name: SECRET_NAME
                  value: 'kaniko-secret'
                - name: REGISTRY_DOCKER_CONFIG_JSON_VALUE
                  value: 'your-value'
                - name: GIT_USERNAME
                  value: 'name'
                - name: GIT_TOKEN
                  value: 'your-token'
                - name: GIT_REPOSITORY_URL_WITHOUT_HTTPS
                  value: '//github.com/user/repo_name.git'
                - name: GIT_REPOSITORY_BRANCH
                  value: 'dev'
                - name: REGISTRY_USERNAME
                  value: 'name'
                - name: IMAGE_NAME
                  value: 'your-image-name'
                - name: IMAGE_VERSION_TAG
                  value: 'your-image-tag'
                - name: PATH_TO_DOCKERFILE
                  value: "Dockerfile"
```