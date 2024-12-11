# github-repo-scanner
This template uses Trivy to scan your private/public GitHub repository.

# Template Parameters
- **GIT_REPO_BRANCH:** The name of the branch you want to scan from your repository.
- **GIT_REPO_URL:** The https clone url of your git repository.
- **GIT_TOKEN:** The token (PAT) of your git.

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
              template: github-repo-scanner
            arguments:
              parameters:
                - name: GIT_REPO_BRANCH
                  value: 'main'
                - name: GIT_REPO_URL
                  value: 'https://github.com/username/repo.git'
                - name: GIT_TOKEN
                  value: 'your-token'
```