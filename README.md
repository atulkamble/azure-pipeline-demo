To set up an **Azure Pipeline** that builds and deploys code from **GitHub**, follow these steps:

---

## **1. Set Up an Azure DevOps Project**
1. Go to **[Azure DevOps](https://dev.azure.com/)**.
2. Create a new **Project**.

---

## **2. Connect Azure Pipelines to GitHub**
1. Go to your **Azure DevOps** project.
2. Navigate to **Pipelines > New Pipeline**.
3. Select **GitHub** as the source.
4. Authenticate and select the **repository**.

---

## **3. Define the `azure-pipelines.yml` File**
Create a `.yml` file in your **GitHub repository** to define the CI/CD pipeline.

### **Basic YAML Pipeline Example**
```yaml
trigger:
- main  # Triggers the pipeline on pushes to the main branch

pool:
  vmImage: 'ubuntu-latest'  # Use a virtual machine for the build

steps:
- task: UseNode@2  # Use Node.js (Optional, change for other languages)
  inputs:
    version: '16.x'

- script: |
    echo Installing dependencies...
    npm install
  displayName: 'Install dependencies'

- script: |
    echo Running tests...
    npm test
  displayName: 'Run tests'

- script: |
    echo Building application...
    npm run build
  displayName: 'Build application'

- task: PublishBuildArtifacts@1  # Upload build artifacts
  inputs:
    pathToPublish: 'dist'
    artifactName: 'drop'
```

---

## **4. Run & Monitor the Pipeline**
1. Commit and push the `.yml` file to GitHub.
2. In **Azure DevOps**, go to **Pipelines** and run the pipeline.
3. Monitor the progress in **Pipelines > Runs**.

---

## **5. Deploy the Code (Optional)**
To deploy to **Azure Web Apps**, **AKS**, or **VMs**, add a deployment task.

### **Example: Deploy to Azure Web App**
```yaml
- task: AzureWebApp@1
  inputs:
    azureSubscription: '<Your Azure Subscription>'
    appName: '<Your Web App Name>'
    package: '$(Build.ArtifactStagingDirectory)/drop'
```

---

## **6. Secure & Automate**
- **Use Secrets:** Store sensitive data in **Azure Key Vault** or **GitHub Secrets**.
- **Branch Policies:** Require checks before merging into `main`.
- **Automate Deployments:** Use **Environments** and **Approvals**.

---

Would you like a specific setup for **.NET, Python, Java, Docker, or Kubernetes**? 🚀
