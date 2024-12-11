# bitbucket-private-repo-scanner
This template uses Trivy to scan your private BitBucket repository.

# Template Parameters
- **GIT_REPO_BRANCH:** The name of the branch you want to scan from your repository.
- **GIT_USERNAME:** The username of your BitBucket.
- **GIT_TOKEN:** The token (App Password) of your BitBucket.
- **BITBUCKET_WORKSPACE_NAME:** The name of the workspace in your BitBucket.
- **GIT_REPO_NAME:** The repository name of your BitBucket

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
        target: repo-scanner
        tasks:
          - name: repo-scanner
            templateRef:
              name: klovercloud-repo-scanner
              template: bitbucket-private-repo-scanner
            arguments:
              parameters:
                - name: GIT_REPO_NAME
                  value: 'basic'
                - name: BITBUCKET_WORKSPACE_NAME
                  value: 'klovercloud'
                - name: GIT_TOKEN
                  value: 'your-token'
                - name: GIT_USERNAME
                  value: 'rafsnil'
                - name: GIT_REPO_BRANCH
                  value: 'master'
```