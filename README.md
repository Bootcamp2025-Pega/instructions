# DevOps in Action: A Hands-On Guide to Building a Modern SDLC

Welcome to the DevOps Bootcamp! This bootcamp is designed to give you hands-on experience with setting up a standard Software Development Life Cycle (SDLC) for a simple application, using GitHub, GitHub Actions, and other free-tier DevOps tools. Over the course of this 3-hour interactive session, you’ll learn how to:

  * Create and manage a GitHub repository.
  * Implement Continuous Integration and Continuous Delivery (CI/CD) pipelines.
  * Deploy applications to free-tier service.

# 1. Requirements

## 1.1. Prerequisites

  * Basic command-line skills: Comfort with navigating directories and running simple commands in a terminal.
  * Git & GitHub basics: Understanding of how to clone a repository, commit changes, and push to a remote branch.

## 1.2. Materials

  * A laptop.
  * A GitHub account (free).
  
  During the workshop we will work on GitHub Codespaces. This ensures everyone has a uniform environment, reducing setup issues.

## 1.3. Technical Setup

Before the bootcamp starts, please ensure the following:

* GitHub Account
  
  Create a free GitHub account if you don’t already have one.

# 2. Agenda

## 2.1. High-level

Below is a high-level breakdown of the 3-hour bootcamp session:
* Introduction to DevOps and the SDLC
* GitHub Repository and Environment Setup
* Implementing CI/CD with GitHub Actions
* Deploying to a Free-Tier Service

## 2.2. Daily Schedule (3-Hour Workshop)

| Time (Approx.) | Activity                                |
| -------------- | --------------------------------------- |
| 0:00 - 0:20    | [SDLC Overview](https://bootcamp2025-pega.github.io/instructions/) |
| 0:20 - 0:30    | GitHub Repository and Environment Setup |
| 0:30 - 2:40    | Implementing CI/CD with GitHub Actions  |
| 2:40 - 3:00    | Summary & Closing Remarks               |

# 3. Steps to Follow

## 3.1. Module 1: DevOps & SDLC Overview

## 3.2. Module 2: Setting Up a GitHub Repository

1.  **Navigate to the Bootcamp Organization**

  *   Go to the [Bootcamp2025-Pega organization on GitHub](https://github.com/Bootcamp2025-Pega).
  
2.  **Navigate to the Instructions Repository**

  *   For detailed instructions, refer to the [instructions repository](https://github.com/Bootcamp2025-Pega/instructions). This is the document you are currently reading.

3.  **Navigate to the bootcamp-blog application repository**

  *  Please see [bootcamp-blog repository](https://github.com/Bootcamp2025-Pega/bootcamp-blog). This is a repository with the application we will be working on. This is an interactive UI-based application where users can post blog messages.

4. **Create your own fork of bootcamp-blog repository**

* **Click the "Fork" button:**  In the top-right corner of the repository page, click the "Fork" button.

  <img src="img/create-fork-button.png" width="250">

  * **Select the organization:** Choose your user space as an organization.
  * **Rename the repository:** In the "Repository name" field, enter the name for the forked repository, following the pattern `bootcamp-blog-{username}`, replacing `{username}` with your GitHub username.

  <img src="img/create-fork.png" width="450">

  * **Create the fork:** Click the "Create fork" button.

5. **Navigate to your repository and get familiar with project**

  * 1. **Navigate to your forked repository:** Go to your personal fork of the `bootcamp-blog` repository (named `bootcamp-blog-{username}`) on GitHub.
  * 2. **Explore the codebase:** Familiarize yourself with the project structure, files, and code.

6. **Run application in Codespaces**

  * **Open Codespaces:** Navigate to your forked `bootcamp-blog-{username}` repository on GitHub. Click on the green "Code" button.
  * **Create new Codespace:** Select the "Codespaces" tab and click on "Create codespace on main". This will start a new cloud-based development environment.
  
  <img src="img/create-codespace.png" width="450">
  
  * **Wait for Codespace to initialize:** GitHub will set up a virtual machine and automatically clone your repository into it. This process may take a few minutes.
  * **Run the application:** Once the Codespace is ready, navigate to a terminal. Run commands:
    
  ```bash
  docker compose up -d
  npm install
  npx prisma db push
  npm run dev
  ```
    
  * **Access the application:** Once the application is running, Codespaces will provide a URL to access it. Go to the **Ports** tab in the bottom panel and find the URL next to port 3000. Click on the URL to open the application in a new browser tab.
  ![Forwarded port](img/codespaces-open-app.png)

  * **Allow log in into dev mode** Copy `Forwarded Address.` Go to `Terminal` tab and close the application (Ctrl^C). Open the .env file and add the following code
    
  ```bash
  NEXTAUTH_URL=<copied_forwarded_address>/api/auth
  NEXTAUTH_SECRET=verystrongsecret
  ```
  Rerun application.

## 3.3. Module 3: Implementing CI/CD with GitHub Actions

### 3.3.1. Basic build pipeline

Goal: Create basic pipeline that builds project and executes tests.

1.  **Create a base workflow**
  * make sure you are on the `main` branch<br>
  `git branch`
  * create a new one<br>
  `git checkout -b add-workflow`
  * create file ci-cd.yaml `mkdir -p .github/workflows && touch .github/workflows/ci-cd.yaml`
  * paste the following into `/.github/workflows/ci-cd.yaml`
  ```yaml
name: CI/CD Pipeline

# Trigger the workflow on push to main and develop branches, and on pull requests
on:
    push:
      tags:
        - '*'
      branches:
        - main
    pull_request:
      branches:
        - main

# Global environment variables
env:
    NODE_VERSION: '18.x'

jobs:
    # Lint & Test Job - Runs on all triggers
    build-and-test:
      name: Build & Test
      runs-on: ubuntu-latest
  
      steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up Node.js ${{ env.NODE_VERSION }}
        uses: actions/setup-node@v3
        with:
          node-version: ${{ env.NODE_VERSION }}
          cache: 'npm'

      - name: Install Dependencies
        run: |
          npm ci

      - name: Build
        run: |
          DISABLE_DB_CONNECTION=true npm run build

  ```
  * commit changes and push to remote<br>
  `git add .`<br>
  `git commit -m "add basic workflow"`<br>
  `git push -u origin add-workflow`

  * head to the URL provided by git
  ![alt text](img/pr-creation-terminal.png)
  * you will see context menu for Pull Request creation<br>
  **IMPORTANT**: set `base` (red box) to point to **your** repo, not the BootCamp one
  ![alt text](img/pr-creation.png)

  * adjust the title / add description and click `Create pull request` button

  * you will see the pull request page. Wait few seconds for **CI/CD Pipeline** check to appear. You can view details of the pipeline run by clicking its name.
  ![alt text](img/pr-overview.png)

  * Once the pipeline will pass, merge the PR (`Merge pull request` button).
  
### 3.3.2. Execute Unit Tests

Unit tests in the project are using jest framework. If you need to run them, just call `npx jest` in terminal.
We need to execute tests in our workflow too. Locate the `steps` list in your GitHub Actions workflow file (`.github/workflows/ci-cd.yml`) and add the following step:

```yaml
      - name: Run tests with coverage
        run: npx jest
```
Create a pull request, wait for validation to pass and merge.

### 3.3.3. Static Code Analysis
#### **SonarCloud**
SonarCloud is a cloud-based service designed to continuosly inspect your code for quality and security issues. What it does:
* Code Quality Analisys: scans code to detect bugs, code smells, and vulnerabilities
* Integration: easy integration with CI/CD pipelines, and tools like Github, Bitbucket, Azure DevOps
* Pull Request decoration: It can provide comments on pull requests with summary of its results
* Dashboard: Detailed dashboard is available

#### **Integrate SonarCloud to your project**
In order to integrate Sonar into your project follow those steps:

1. Go to SonarCould [login page](https://sonarcloud.io/login)

1. Choose login with Github
![Login with Github](img/sonar-loging1.png)

1. Grand SonarQubeCloud necessary permissions to your project
![Sonar permisions](img/sonar-authorize.png)

1. Configure project binding on the GitHub side. Navigate to https://github.com/<github_username>/bootcamp-blog-<github_username>/settings/installations and ensure the **SonarQubeCloud** is configured properly: check `Repository access` section and verify that your project access is granted.

1. Generate token. In order to connect Github and Sonar you need to generate token:
    * First go to My Account  

1. Click on + sign and choose Analyze new project
    
    ![Sonar add](img/sonar-add-org1.png)

1. Choose "Import another organization"

    ![Sonar add 2](img/sonar-add-org2.png)

1. Import from Github

    ![Sonar add 3](img/sonar-add-org3.png)

1. Choose GitHub

    ![Sonar add 4](img/sonar-add-org4.png)

1. Choose your **private account**

    ![Sonar add 5](img/sonar-add-org5.png)

1. Choose free plan and create organization

1. Analyse new project

    ![Sonar add 6](img/sonar-add-org6.png)

1. Choose your repository and set it up

    ![Sonar add 7](img/sonar-add-org7.png)

1. Choose Previous version and create project

    ![Sonar add 8](img/sonar-add-org8.png)

1. Generate token. In order to connect Github and Sonar you need to generate token:
    * First go to My Account

        ![My Acocunt](img/generate-token-account.png)
    * Go to Security tab, enter token name of your choosing, generate token

        ![Security tab](img/sonar-generating-token.png)

    * Now you need to add token to Github secrets (`SONAR_TOKEN`). Enter name and contents of your secret.

        ![Github token](img/sonar-adding-token.png) 

1. Disable SonarCloud Automatic Analysis

    While SonarCloud offers automatic analysis for imported projects (which provides quick setup and immediate feedback), we'll disable this feature to manually control our analysis process through CI/CD:

    - Navigate to your SonarCloud project analysis settings:
      ```
      https://sonarcloud.io/project/analysis_method?id=<github_username>_bootcamp-blog-<github_username>
      ```

    - Find the "Automatic Analysis" section and disable it:
      
      ![Disable Automatic Analysis](docs/img/sonar-disable-auto.png)

    - Click "Save" to confirm your changes

    This configuration allows us to:
    - Run custom analysis steps in our CI pipeline
    - Include test coverage data from our Jest tests
    - Have more control over the scanning process
    - Upload results manually from our GitHub Actions workflow

    Now SonarCloud will only analyze your code when we explicitly trigger analysis through our CI/CD pipeline.


1. Configure project by providing sonar settings file.

    Create a file named `sonar-project.properties` in the root of your project with the following content:

      ```properties
      # Organization name: github username or organization, if repo is assigned to one
      sonar.organization=<github_username>
      # Project key on sonar. Default is <org_name>_<your-repo-name>
      sonar.projectKey=<github_username>_bootcamp-blog-<github_username>
      
      # Sources
      sonar.sources=.
      sonar.exclusions=**/__tests__/**/*,**/*.test.js,**/*.spec.js
      
      # Tests
      sonar.tests=.
      sonar.test.inclusions=**/__tests__/**/*,**/*.test.js,**/*.spec.js
    ```

1. Configure Sonar Scan Action in your workflow. Add the following step:

    ```yaml
        - name: Sonar Scan
          uses: SonarSource/sonarqube-scan-action@v5.0.0
          env:
            SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
    ```

17. You are all set. On your workflow run, sonar scan will be executed and published to the repository.

### 3.3.4. Test Coverage

In order to capture test coverage, we need to enable it alongside tests.

Add the following content to `module.exports` in the `jest.config.js` file on the ROOT of your project:
```js
  collectCoverage: true,
  coverageDirectory: 'coverage',
  coverageReporters: ['lcov', 'text']
```
This ensures that coverage is captured.

| **lcov** format is a standard coverage format understood by sonar.

To ensure SonarCloud correctly analyzes your code coverage reports, 
update sonar-project.properties file and set the paths to `lcov` file:
  
  ```properties
  sonar.javascript.lcov.reportPaths=coverage/lcov.info
  sonar.coverage.exclusions=**/__tests__/**/*,**/*.test.js,**/*.spec.js
  ```

Verify Configuration. After your workflow completes:
  - Check your SonarCloud dashboard
  - Verify coverage metrics are displayed
  - Review the code quality and coverage insights

This integration will help you track code quality and ensure adequate test coverage for your application.

### 3.3.5. Static Application Security Testing (SAST)
1. On GitHub, navigate to the main page of the repository.
2. Under your repository name, click  Settings. If you cannot see the "Settings" tab, select the  dropdown menu, then click Settings.
3. In the "Security" section of the sidebar, click  Code security.
4. In the "Code scanning" section, select Set up , then click Default.
You will then see a "CodeQL default configuration" dialog summarizing the code scanning configuration automatically created by default setup.
5. Review the settings for default setup on your repository, then click Enable CodeQL. This will trigger a workflow that tests the new, automatically generated configuration.

Detailed instruction explaining above steps can be found in [GitHub doc](https://docs.github.com/en/code-security/code-scanning/enabling-code-scanning/configuring-default-setup-for-code-scanning#configuring-default-setup-for-a-repository)

6. Checkout to new branch
7. Add below code block to `handle(req, res)` method in [pages/api/publish/[id].ts](https://github.com/Bootcamp2025-Pega/bootcamp-blog/blob/main/pages/api/publish/%5Bid%5D.ts)
```ts
  const { url } = req.query;
  try {
    // Make a GET request to the provided URL
    const response = await fetch(url);
    if (!response.ok) {
      console.error("Something went wrong...");
    }
  } catch (error) {
    console.error(error);
  }
```
  It should look like this:
![Vulnerability example](img/sast/code_snippet01.png)

8. Push changes to remote brach and create a Pull Request
9. Wait for CodeQL analysis to finish and review issue found.
10. Discard the PR (it's vulnerable!)


### 3.3.6. Software Composition Analysis (SCA)
1. Go to Security tab in your Gtihub repository
2. Click "Enable Dependabot alerts"
![alt text](img/sast/dependabot01.png)
3. Click "Enable" on **Dependabot Alerts** and **Dependabot security updates**
![alt text](img/sast/dependabot02.png)
4. Go back to Security tab and review Dependabot findings 
![alt text](img/sast/dependabot03.png)
Additionally, Pull Request should be automatically created that updates vulnerable library to vulnerability-free version.

### 3.3.7. Releasing stable version
After itegrating bunch of changes to `main`, you've finished working on a feature(s) and you need to release a new version. 
* Go to main view of your repository, on the right-side you'll see `Releases` section. Click on the link <br>
![alt text](img/releases.png)
* Type tag name (e.g. v0.1.0), title and description containing changes introduced in new Release. After clicking `Publish release`, GitHub will create new tag (with name you've provided) and will trigger your workflow.<br>
![alt text](img/releases-page.png)
* You can then view your release along with its assets
![alt text](img/releases-final.png)

### Wrap-up
At this point you have working CI pipeline that executes tests, measures coverage and performs static analysis. There is one problem though - nothing blocks you from merging invalid PRs.

**TASK:** allow merging **only if** build will pass green.

## 3.4 Module 4: Deployment to Free-Tier Service

### 3.4.1 How to Create an Account on Vercel

This guide will walk you through the steps to create an account on Vercel.

### 3.4.1.1. Sign Up Options

You can sign up for a Vercel account using the following methods:
- **Email**: Use your email address to create an account.
- **Git Providers**: Sign up using GitHub, GitLab, or Bitbucket.
- **Passkeys**: Use passkeys for login, which include biometric methods or hardware security keys.

***In our case, we will focus on Signing Up with Email***

### 3.4.1.2. Signing Up with Email

1. Enter your email address on the [Vercel sign-up page](https://vercel.com).
![SignUp](img/vercel-signup.png)
![SignUp2](img/vercel-signup2.png)
![SignUp3](img/vercel-signup3.png)

2. You will receive a six-digit One-Time Password (OTP) to your email.
![SignUp](img/vercel-signup4.png)
3. Enter the OTP to complete the sign-up process.

> **Note**: No Git provider is connected by default when using email. You will need to verify your account on every login.


---

For more details, visit the [Vercel Documentation](https://vercel.com/docs/accounts/create-an-account).


### 3.4.2 How to Get a Vercel API Access Token

This guide explains the steps to create and manage a Vercel API Access Token.

### 3.4.2.1. Navigate to Account Settings

1. Log in to your Vercel account.
2. In the top-right corner of the dashboard, click on your profile picture.
3. Select **Settings** from the dropdown menu.

### 3.4.2.2. Access the Tokens Section

1. In the **Account Settings** page, locate the **Tokens** section in the sidebar.
2. Click on **Tokens** to open the token management page.

### 3.4.2.3. Create a New Access Token

1. In **Create token** section:
2. Enter a descriptive name for your token.
![Token](img/vercel-token.png)
3. Choose the scope of access for the token:
   - Personal Account
   - Specific Teams (if applicable)
4. Set an expiration date for the token (optional but recommended for security).
5. Click **Create** to generate the token.
6. Please copy your token and store it in a safe place.
For security reasons, you are not able to see it again.

> **Important**: Make a note of the token immediately after creation, as it will not be displayed again.

### 3.4.2.4. Use the Access Token

This guide explains how to securely store access token, in your GitHub repository using repository secrets.

### 3.4.2.4.1. Navigate to Your Repository Settings

1. Go to the main page of your GitHub repository.
2. Under your repository name, click on **Settings**.

### 3.4.2.4.2. Access the Secrets Section

1. In the **Settings** sidebar, locate the **Security** section.
2. Click on **Secrets and variables**, then select **Actions**.

### 3.4.2.4.3. Add a New Repository Secret

1. Click the **New repository secret** button.
2. In the **Name** field, enter a name for your secret: `VERCEL_TOKEN`.
3. In the **Secret** field, paste the value of your secret.
4. Click **Add secret** to save it.


### 3.4.3. How to set up your Vercel Postgres database


This guide explains the steps to set up a Vercel Postgres database for your project.

### 3.4.3.1. Access the Storage Tab

1. Log in to your Vercel account.
2. Navigate to your project dashboard.
3. Select the **Storage** tab from the project settings.

### 3.4.3.2. Create a New Database

1. Select **Neon Serverless Postgres** from the list and click **Create**.

![db1](img/vercel-db1.png)

2. On the **Create Database** form , select `Region` and `Installation plan`.

![db2](img/vercel-db2.png)

3. Click **Continue** to proceed.

### 3.4.3.3. Configure the Database

1. Enter a name for your database (e.g., `my_postgres_db`).
   - The name can only contain alphanumeric characters, underscores (`_`), and hyphens (`-`).
   - It must not exceed 32 characters.
2. Click **Create** to finalize the setup.

### 3.4.4. Environment Variables

1. Once the database is created, Vercel automatically adds environment variables to your project:

![db3](img/vercel-db3.png)
  
> **Important**: We just created db but is  it not connected to any project yet.


### 3.4.5. How to add your GitHub project to Vercel and connect to database


This guide explains the steps to connect your GitHub project with arleady created db.

### 3.4.5.1. Link project

1. Go to your GitHub project, open `Codespaces`.
2. Export VERCEL_TOKEN
```bash
export VERCEL_TOKEN=<past_your_vercel_token>
echo $VERCEL_TOKEN
```
3. Install Vercel cli and link your project
```bash
npm i -g vercel
vercel --version
vercel link --token=$VERCEL_TOKEN
```
Accept default values. After finishing you should see:
![link](img/vercel-link.png)

### 3.4.5.2. Add secrets to your GiHub project

1. Go to directory `.vercel` and open file `project.json`
2. Add next secrets into you GitHub project:
- `VERCEL_PROJECT_ID` - copy value from `project.json` file from key `projectId`
- `VERCEL_ORG_ID` - copy value from `project.json` file from key `orgId`

### 3.4.5.3. Connect project to database

1. Go to your Vercel page, go to `Storage` and click button `Connect Project`
![connect-project1](img/connect-project1.png)
![connect-project2](img/connect-project2.png)
Select proper values and click `Connect`

### 3.4.5.4. Export env variables

1. Back to `Codespaces` and execute command
```bash
vercel env pull .env --token=$VERCEL_TOKEN 
```
`.env` file should be generated.
We now have a fully functioning Vercel Postgres database and have all the environment variables to run it locally and on Vercel.

### 3.4.6. Setup Prisma and create the database schema

This guide explains the steps to setup Prisma and create database schema.

### 3.4.6.1. Install Prisma

1. Go to `Codespaces` and execute command
```bash
npm i prisma --save-dev --legacy-peer-deps
npm i @prisma/client@6.5.0 --legacy-peer-deps
```

### 3.4.6.2. Generate schema

1. Prisma schema defines two models into direcotry `prisma`, each of which will map to a table in the underlying database: User and Post.
To actually create the tables in your database, you now can use the following command:
```bash
npx prisma db push
```
You should see following output:
![prisma-1](img/prisma1.png)


### 3.4.7.  Creating OAuth Apps in GitHub

To create an OAuth app in GitHub, follow these steps:

### 3.4.7.1. Navigate to GitHub Settings

1. Go to GitHub and log in to your account.
2. In the upper-right corner of any page, click your profile photo, then click **Settings**.

### 3.4.7.2. Register a New OAuth Application

1. In the left sidebar, click **Developer settings**.
2. In the left sidebar, click **OAuth Apps**.
3. Click **New OAuth App**.
![oauth1-1](img/oauth1.png)

### 3.4.7.3. Fill in the Application Details

1. **Application name**: Enter a name for your application. This name will be displayed to users when they are asked to grant access to your application `<project name>.vercel.app`.
2. **Homepage URL**: Enter the URL of your application's homepage `https://<project name>.vercel.app`.
3. **Authorization callback URL**: Enter the URL where users will be sent after they authorize with GitHub. This URL should be a route in your application that handles the OAuth callback. `https://<project name>.vercel.app/api/auth/callback/github`
![oauth1-1](img/oauth3.png)

### 3.4.7.4. Register the Application

1. Click **Register application**.
2. After registering, you will be redirected to the application's page where you can see the **Client ID** and **Client Secret**. These credentials are used to authenticate your application with GitHub.

### 3.4.7.5 Configure Environment Variables

1. In your GitHub project, store the **Client ID** and **Client Secret** as secret variables:
 - NEXTAUTH_URL = `https://<project name>.vercel.app/api/auth`
 - OAUTH_SECRET =  paste e.g. `verystrongsecret`
 - OAUTH_GITHUB_ID = **Client ID**
 - OAUTH_GITHUB_SECRET = **Client Secret**
 ![oauth1-1](img/oauth4.png)


### 3.4.8. Basic deployment pipeline
Goal: Create basic deployment pipeline that deploy project on Vercel platform.

### 3.4.8.1. Create a deployment workflow
make sure you are on the main branch
```bash
git branch
```

create a new one
```bash
git checkout -b add-workflow-deployment
```bash
create file .yaml 
```bash
mkdir -p .github/workflows && touch .github/workflows/production.yaml
```
paste the following into /.github/workflows/production.yaml
```bash
name: Vercel Production Deployment
env:
  VERCEL_ORG_ID: ${{ secrets.VERCEL_ORG_ID }}
  VERCEL_PROJECT_ID: ${{ secrets.VERCEL_PROJECT_ID }}
  GITHUB_ID: ${{ secrets.OAUTH_GITHUB_ID }}
  GITHUB_SECRET: ${{ secrets.OAUTH_GITHUB_SECRET }}
  NEXTAUTH_SECRET: ${{ secrets.OAUTH_SECRET }}
  NEXTAUTH_URL: ${{ secrets.NEXTAUTH_URL }}

on:
  push:
    tags:
      - '*'
jobs:
  Deploy-Production:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Install Vercel CLI
        run: npm i -g vercel
      - name: Set Environment Variables
        run: |
            echo -n $GITHUB_ID | vercel env add GITHUB_ID production --token=${{ secrets.VERCEL_TOKEN }}
            echo -n $GITHUB_SECRET | vercel env add GITHUB_SECRET production --token=${{ secrets.VERCEL_TOKEN }}
            echo -n $NEXTAUTH_SECRET | vercel env add NEXTAUTH_SECRET production --token=${{ secrets.VERCEL_TOKEN }}
            echo -n $NEXTAUTH_URL | vercel env add NEXTAUTH_URL production --token=${{ secrets.VERCEL_TOKEN }} 
      - name: Pull Vercel Environment Information
        run: vercel pull --yes --environment=production --token=${{ secrets.VERCEL_TOKEN }}
      - name: Build Project Artifacts
        run: vercel build --prod --token=${{ secrets.VERCEL_TOKEN }}
      - name: Deploy Project Artifacts to Vercel
        run: vercel deploy --prebuilt --prod --token=${{ secrets.VERCEL_TOKEN }}
```
commit changes and push to remote
```bash
git add .
git commit -m "add deployment workflow"
git push -u origin add-workflow-deployment
```

head to the URL provided by git:

you will see context menu for Pull Request creation<br>
**IMPORTANT**: set `base` (red box) to point to **your** repo, not the BootCamp one
![alt text](img/pr-creation.png)

adjust the title / add description and click `Create pull request` button

you will see the pull request page. Wait few seconds for **CI/CD Pipeline** check to appear. You can view details of the pipeline run by clicking its name.
![alt text](img/pr-overview.png)

Once the pipeline will pass, merge the PR (`Merge pull request` button).

Every time a tag is created, a workflow will be started that will deploy the tag version to production. Once the deployment.yaml workflow is completed, we can access the production application using the link `https://<project name>.vercel.app`
