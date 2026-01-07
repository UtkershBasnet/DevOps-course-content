#### Date: 7th January 2026
# Add an Agent and Implement the CD

## 1. What is a CI/CD Agent/Runner?
An agent (or runner) is a software application that runs the jobs defined in 
your CI/CD pipeline. 
- **Managed Runners:** Provided by the CI/CD platform (e.g., GitHub-hosted 
  runners). They are easy to use but have limits on customization and 
  performance.
- **Self-Hosted Runners:** Servers you manage yourself (on-premise or in the 
  cloud) that you register with your CI/CD platform. They offer more 
  control, better performance, and access to internal network resources.

## 2. Why use Self-Hosted Agents?
- **Cost:** Can be cheaper if you already have idle server capacity.
- **Customization:** Install specific software, libraries, or configurations 
  not available on managed runners.
- **Security/VPN:** Agents can access internal databases or servers that are 
  not exposed to the public internet.
- **Persistence:** Cache large build dependencies across different job runs.

## 3. Setting Up a GitHub Actions Self-Hosted Runner
1. **Prepare the Host:** A Linux, Windows, or macOS machine.
2. **Download the Runner:** Go to Repo Settings -> Actions -> Runners -> 
   New self-hosted runner.
3. **Configure:** Run the provided configuration script with the registration 
   token.
4. **Run:** Start the runner service (e.g., `./run.sh`).
5. **Labels:** Assign labels to your runner (e.g., `production`, `high-mem`) 
   to target specific jobs to it.

## 4. Implementing the CD (Continuous Deployment)
Continuous Deployment automates the release of a project to a production-like 
environment. For a containerized app on Kubernetes, this usually involves:
1. **Building the Image:** In the CI stage.
2. **Pushing to Registry:** (e.g., Docker Hub, ECR).
3. **Updating K8s Manifests:** Changing the image tag in the deployment YAML.
4. **Applying Changes:** Using `kubectl apply` or a GitOps tool like ArgoCD.

## 5. A Simple CD Workflow Example
```yaml
name: Deployment
on:
  push:
    branches: [ main ]
jobs:
  deploy:
    runs-on: self-hosted # Use our custom agent
    steps:
      - name: Checkout Code
        uses: actions/checkout@v4
      - name: Login to Docker Hub
        run: echo "${{ secrets.DOCKER_PASSWORD }}" | docker login -u user --password-stdin
      - name: Build and Push
        run: |
          docker build -t myapp:${{ github.sha }} .
          docker push myapp:${{ github.sha }}
      - name: Deploy to K8s
        run: |
          sed -i 's|IMAGE_TAG|'${{ github.sha }}'|g' k8s/deployment.yaml
          kubectl apply -f k8s/deployment.yaml
```

## 6. Deployment Strategies for CD
- **Blue-Green Deployment:** Run two identical production environments. Swap 
  traffic to the new version (Green) only after successful testing.
- **Canary Release:** Deploy the new version to a small subset of users 
  initially. Monitor for errors before rolling out to everyone.

## 7. Best Practices for CD Agents
- **Security:** Ensure agents are isolated and have only the permissions 
  needed. Use specific IAM roles for cloud-based agents.
- **Maintenance:** Regularly update the runner software and its underlying OS.
- **Scaling:** Use "Ephemeral Runners" that spin up for a job and shut down 
  immediately after (e.g., Actions Runner Controller for K8s).

## 8. Conclusion
Moving from CI to CD requires robust infrastructure. Setting up your own 
agents gives you the power and flexibility needed to automate complex 
deployments, ensuring that your code reaches production safely and 
efficiently every time.

---
*End of Notes*
