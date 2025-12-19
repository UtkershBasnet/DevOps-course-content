#### Date: 19th December 2025
# A Simple CI Using GitHub Actions

## 1. What is GitHub Actions?
GitHub Actions is a continuous integration and continuous delivery (CI/CD) 
platform that allows you to automate your build, test, and deployment 
pipeline. You can create workflows that build and test every pull request to 
your repository, or deploy merged pull requests to production.

## 2. Core Concepts of GitHub Actions
- **Workflow:** A configurable automated process that will run one or more 
  jobs. Defined by a YAML file in your repository.
- **Event:** A specific activity in a repository that triggers a workflow run 
  (e.g., `push`, `pull_request`, `schedule`).
- **Job:** A set of steps in a workflow that is executed on the same runner. 
  Jobs can run in parallel or sequentially.
- **Step:** An individual task that can run commands in a job. A step can be 
  an action or a shell command.
- **Action:** A standalone command that is combined into steps to create 
  a job. Actions are the smallest portable building block of a workflow.
- **Runner:** A server that runs your workflows when they're triggered. Each 
  runner can run a single job at a time.

## 3. Workflow File Structure
Workflows are stored in the `.github/workflows` directory of your repository.
```yaml
name: CI Example
on: [push] # Trigger on every push
jobs:
  build:
    runs-on: ubuntu-latest # The type of runner
    steps:
      - name: Checkout Code
        uses: actions/checkout@v4
      - name: Run a Script
        run: echo "Hello, GitHub Actions!"
```

## 4. Building a Simple Node.js CI
```yaml
name: Node.js CI
on:
  push:
    branches: [ main ]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4
    - name: Use Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '20'
    - run: npm install
    - run: npm test
```

## 5. Environment Variables and Secrets
- **Variables:** Used for non-sensitive info (e.g., API URLs).
- **Secrets:** Used for sensitive information (e.g., passwords, API keys). 
  Accessed via `${{ secrets.MY_SECRET }}`.
- Defined in GitHub Repository Settings -> Secrets and variables -> Actions.

## 6. Matrix Builds
Allows you to test your code on multiple versions of a language or multiple 
operating systems simultaneously:
```yaml
strategy:
  matrix:
    node-version: [16, 18, 20]
    os: [ubuntu-latest, windows-latest]
```

## 7. Artifacts and Caching
- **Artifacts:** Persist files (e.g., build binaries) after a job has 
  completed so you can share them with another job or download them.
- **Caching:** Speed up your jobs by reusing files from a previous run 
  (e.g., `node_modules`).

## 8. Conclusion
GitHub Actions makes it incredibly easy to implement CI/CD directly within 
your version control system. Its native integration, large marketplace of 
pre-built actions, and flexible YAML configuration make it a top choice for 
modern DevOps teams.

---
*End of Notes*
