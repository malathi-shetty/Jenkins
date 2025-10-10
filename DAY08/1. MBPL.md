# **Multibranch Pipeline in Jenkins**

A **Multibranch Pipeline** in Jenkins is used to automatically create and manage pipelines for different branches of a repository. It helps in **CI/CD automation** by dynamically detecting branches and running pipelines based on branch-specific Jenkinsfiles.

---

## **1. Why Use a Multibranch Pipeline?**
- **Automatic Branch Detection**: When new branches are created in a repository, Jenkins automatically detects them and sets up a pipeline.
- **Branch-Specific Pipelines**: Each branch can have a different `Jenkinsfile`, allowing for customized builds per branch.
- **Supports Feature Branch Workflows**: Ideal for **Git Flow**, **GitHub Flow**, or any branching strategy.
- **Automatic Cleanup**: Old or deleted branches are removed from Jenkins to keep things organized.

---

## **2. How Multibranch Pipeline Works**
- Jenkins scans a **Git repository** for branches.
- If a branch contains a `Jenkinsfile`, Jenkins creates a pipeline for that branch.
- When changes are pushed to any branch, Jenkins triggers a build.

---

## **3. Setting Up a Multibranch Pipeline**

### **Step 1: Install Required Plugins**
- Jenkins comes with **Pipeline** support, but make sure you have:
  - **Pipeline** Plugin
  - **Multibranch Pipeline** Plugin
  - **Git** Plugin (or GitHub, Bitbucket plugins based on your repo)

### **Step 2: Create a Multibranch Pipeline Job**
1. **Go to Jenkins Dashboard** → Click **New Item**.
2. Enter a name (e.g., `MyProject-Multibranch`).
3. Select **Multibranch Pipeline** and click **OK**.

### **Step 3: Configure the Multibranch Pipeline**
1. **Under “Branch Sources”**, click **Add Source** → **Git** or **GitHub**.
2. Enter the repository URL (e.g., `https://github.com/your-repo.git`).
3. Add credentials (if required) for private repositories.
4. Configure the **Discovery** settings:
   - Discover all branches (`*`).
   - Optionally, filter to specific branches (e.g., `feature/*` or `release/*`).

### **Step 4: Define a `Jenkinsfile` in Each Branch**
Each branch must have a `Jenkinsfile` that defines the pipeline.

**Example `Jenkinsfile` for a simple CI/CD pipeline:**
```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
            }
        }
    }
}
```

### **Step 5: Save and Scan Repository**
1. Click **Save**.
2. Click **Scan Repository Now** under “Scan Multibranch Pipeline Log”.
3. Jenkins will discover branches with `Jenkinsfile` and create pipelines.

---

## **4. Running a Multibranch Pipeline**
- When Jenkins detects a new branch with a `Jenkinsfile`, it automatically **creates a new pipeline**.
- When a commit is pushed, Jenkins triggers a **build** for that specific branch.
- Deleted branches are automatically removed from Jenkins.

---

## **5. Advanced Features**

### **1. PR (Pull Request) Support**
- If using **GitHub** or **Bitbucket**, you can configure **Pull Request discovery**.
- Jenkins can trigger pipelines **only for PRs**.

### **2. Custom Jenkinsfile Per Branch**
- You can specify different `Jenkinsfile` locations:
  ```groovy
  Script Path: my-custom-Jenkinsfile
  ```
- Useful if different branches have different build requirements.

### **3. Cleanup Old Branches**
- Configure **Orphaned Item Strategy** to automatically delete jobs for deleted branches.
- Example:
  - Remove after **30 days** of inactivity.

---

## **6. Best Practices**
✅ Keep the `Jenkinsfile` at the **root** of the repository.  
✅ Use environment variables for credentials (`withCredentials`).  
✅ Enable **webhooks** in GitHub/GitLab/Bitbucket to trigger builds instantly.  
✅ Archive build artifacts for debugging (`archiveArtifacts`).  
✅ Use **Branch Filtering** (`feature/*`, `release/*`) to avoid unnecessary pipelines.

---

## **7. Summary**
- **Multibranch Pipeline** automates CI/CD for multiple branches.
- Jenkins dynamically **detects** and **builds** branches with a `Jenkinsfile`.
- Supports **PR validation**, **feature branch workflows**, and **automatic cleanup**.
- Easy to **set up** and **scale** for large repositories.


