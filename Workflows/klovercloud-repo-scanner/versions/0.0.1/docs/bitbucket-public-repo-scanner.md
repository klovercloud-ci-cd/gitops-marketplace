# bitbucket-public-repo-scanner
This template uses Trivy to scan your private BitBucket repository.

# Template Parameters
- **GIT_REPOSITORY_BRANCH:** The name of the branch you want to scan from your repository.
- **BITBUCKET_WORKSPACE_NAME:** The name of the workspace in your BitBucket.
- **GIT_REPOSITORY_NAME:** The repository name of your BitBucket

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
              template: bitbucket-public-repo-scanner
            arguments:
              parameters:
                - name: GIT_REPOSITORY_NAME
                  value: 'basic'
                - name: BITBUCKET_WORKSPACE_NAME
                  value: 'klovercloud'
                - name: GIT_REPOSITORY_BRANCH
                  value: 'master'
```