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

* Share your GitHub username with the Bootcamp organizers so they can add you to the Bootcamp2025-Pega organization.

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
| 0:00 - 0:10    | Welcome                                 |
| 0:10 - 0:20    | [SDLC Overview](https://bootcamp2025-pega.github.io/instructions/) |
| 0:20 - 0:30    | GitHub Repository and Environment Setup |
| 0:30 - 2:00    | Implementing CI/CD with GitHub Actions  |
| 2:00 - 2:30    | Deployment                              |
| 2:30 - 2:40    | Summary & Closing Remarks               |

# 3. Steps to Follow

## 3.1. Module 1: DevOps & SDLC Overview

## 3.2. Module 2: Setting Up a GitHub Repository

1.  **Navigate to the Bootcamp Organization**

  *   Go to the [Bootcamp2025-Pega organization on GitHub](https://github.com/Bootcamp2025-Pega).
  *   If you've provided your GitHub username to the organizers, you should already be a member. If not, please inform the organizers to be added.
  
2.  **Navigate to the Instructions Repository**

  *   For detailed instructions, refer to the [instructions repository](https://github.com/Bootcamp2025-Pega/instructions). This is the document you are currently reading.

3.  **Navigate to the movie-night-planner application repository**

  *  Please see [movie-night-planner repository](https://github.com/Bootcamp2025-Pega/movie-night-planner). This is a repository with the application we will be working on. This is an interactive UI-based application where users can build and manage a personal movie watchlist.

4. **Create your own fork of movie-night-planner repository**

   * 1. **Click the "Fork" button:**  In the top-right corner of the repository page, click the "Fork" button.
  ![Create a fork button](img/create-fork-button.png)
   * 3. **Select the organization:** Choose the organization **Bootcamp2025-Pega** to fork the repository into.
   * 4. **Rename the repository:** In the "Repository name" field, enter the name for the forked repository, following the pattern `movie-night-planner-{username}`, replacing `{username}` with your GitHub username.
  ![Create a fork](img/create-fork.png)
   * 5. **Create the fork:** Click the "Create fork" button.

5. **Navigate to your repository and get familiar with project**

  * 1. **Navigate to your forked repository:** Go to your personal fork of the `movie-night-planner` repository (named `movie-night-planner-{username}`) on GitHub.
  * 2. **Explore the codebase:** Familiarize yourself with the project structure, files, and code. Pay attention to the `README.md` file, which provides an overview of the application.

6. **Run application in Codespaces**

    * 1.  **Open Codespaces:** Navigate to your forked `movie-night-planner-{username}` repository on GitHub. Click on the green "Code" button.
    * 2.  **Create new Codespace:** Select the "Codespaces" tab and click on "Create codespace on main". This will start a new cloud-based development environment.
    ![Create codespace](img/create-codespace.png)
    * 3.  **Wait for Codespace to initialize:** GitHub will set up a virtual machine and automatically clone your repository into it. This process may take a few minutes.
    * 4.  **Run the application:** Once the Codespace is ready, navigate to a terminal. Run commands:
    ```bash
    # Run backend
    cd backend && docker-compose up
    # Run frontend
    cd .. && npm run dev
    ```
    
    **TODO**
    
    * 5.  **Access the application:** Once the application is running, Codespaces will provide a URL to access it. Check the terminal output for the URL. Click on the URL to open the application in a new browser tab.
    ![Forwarded port](img/forwarded-port.png) (**TODO**).

## 3.3. Module 3: Implementing CI/CD with GitHub Actions

# TODO

### 3.3.1. Basic build pipeline

Goal: Create basic pipeline that builds project and execute tests.

1.  **Create a base workflow**


  
### 3.3.2. Execute Unit Tests

### 3.3.3. Verify pull request

### 3.3.4. Static Code Analysis
#### **SonarCloud**
SonarCloud is a cloud-based service designed to continuosly inspect your cose for quality and security issues. What it does:
* Code Quality Analisys: scans code to detect bugs, code smells, and vulnerabilities
* Integration: easy integration with CI/CD pipelines, and tools like Github, Bitbucket, Azure DevOps
* Pull Request decoration: It can provide comments on pull requests with summary of its results
* Dashboard: Detailed dashboard is available

#### **Integrate SonarCloud to your project**
In order to integrate Sonar into your project follow those steps:
1. Go to SonarCould [login page](https://sonarcloud.io/login)
2. Choose login with Github
![Login with Github](img/sonar-loging.png)
3. Grand SonarQubeCloud necessary permissions
![Sonar permisions](img/sonar-authorize.png)
4. Connect to bootcamp org //TODO!
5. Generate token. In order to connect Github and Sonar you need to generate token:
* First go to My Account
![My Acocunt](img/generate-token-account.png)
* Go to Security tab, enter token name of your choosing, generate token
![Security tab](img/sonar-generating-token.png)
6. Now you need to add token to Github secrets. Enter name and contents of your secret.
![Github token](img/sonar-adding-token.png)
7. You are all set!


### 3.3.5. Test Coverage

### 3.3.6. ...

### 3.3.6. Static Application Security Testing (SAST)

### 3.3.7. Software Composition Analysis (SCA)

### 3.3.8. ...

## 3.4 Module 4: Deployment to Free-Tier Service
# How to Create an Account on Vercel

This guide will walk you through the steps to create an account on Vercel.

### 1. Sign Up Options

You can sign up for a Vercel account using the following methods:
- **Email**: Use your email address to create an account.
- **Git Providers**: Sign up using GitHub, GitLab, or Bitbucket.
- **Passkeys**: Use passkeys for login, which include biometric methods or hardware security keys.

***In our case, we will focus on Signing Up with Email***

### 2. Signing Up with Email

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


# How to Get a Vercel API Access Token

This guide explains the steps to create and manage a Vercel API Access Token.

### 1. Navigate to Account Settings

1. Log in to your Vercel account.
2. In the top-right corner of the dashboard, click on your profile picture.
3. Select **Settings** from the dropdown menu.

### 2. Access the Tokens Section

1. In the **Account Settings** page, locate the **Tokens** section in the sidebar.
2. Click on **Tokens** to open the token management page.

### 3. Create a New Access Token

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

### 4. Use the Access Token

This guide explains how to securely store access token, in your GitHub repository using repository secrets.

#### 4.1. Navigate to Your Repository Settings

1. Go to the main page of your GitHub repository.
2. Under your repository name, click on **Settings**.

### 4.2. Access the Secrets Section

1. In the **Settings** sidebar, locate the **Security** section.
2. Click on **Secrets and variables**, then select **Actions**.

### 4.3. Add a New Repository Secret

1. Click the **New repository secret** button.
2. In the **Name** field, enter a name for your secret: `VERCEL_TOKEN`.
3. In the **Secret** field, paste the value of your secret.
4. Click **Add secret** to save it.


# How to set up your Vercel Postgres database


This guide explains the steps to set up a Vercel Postgres database for your project.

### 1. Access the Storage Tab

1. Log in to your Vercel account.
2. Navigate to your project dashboard.
3. Select the **Storage** tab from the project settings.

### 2. Create a New Database

1. Select **Neon Serverless Postgres** from the list and click **Create**.

![db1](img/vercel-db1.png)

2. On the **Create Database** form , select `Region` and `Installation plan`.

![db2](img/vercel-db2.png)

3. Click **Continue** to proceed.

### 3. Configure the Database

1. Enter a name for your database (e.g., `my_postgres_db`).
   - The name can only contain alphanumeric characters, underscores (`_`), and hyphens (`-`).
   - It must not exceed 32 characters.
2. Click **Create** to finalize the setup.

### 4. Environment Variables

1. Once the database is created, Vercel automatically adds environment variables to your project:

![db3](img/vercel-db3.png)
  
> **Important**: We just created db but is  it not connected to any project yet.


# How to add your GitHub project to Vercel and connect to database


This guide explains the steps to connect your GitHub project with arleady created db.

### 1. Link project

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

### 2. Add secrets to your GiHub project

1. Go to directory `.vercel` and open file `project.json`
2. Add next secrets into you GitHub project:
- `VERCEL_PROJECT_ID` - copy value from `project.json` file from key `projectId`
- `VERCEL_ORG_ID` - copy value from `project.json` file from key `orgId`

### 3. Connect project to database

1. Go to your Vercel page, go to `Storage` and click button `Connect Project`
![connect-project1](img/connect-project1.png)
![connect-project2](img/connect-project2.png)
Select proper values and click `Connect`

### 4. Export env variables

1. Back to `Codespaces` and execute command
```bash
vercel env pull .env --token=$VERCEL_TOKEN 
```
`.env` file should be generated.
We now have a fully functioning Vercel Postgres database and have all the environment variables to run it locally and on Vercel.

# Setup Prisma and create the database schema

This guide explains the steps to setup Prisma and create database schema.

### 1. Install Prisma

1. Go to `Codespaces` and execute command
```bash
npm i prisma --save-dev --legacy-peer-deps
npm i @prisma/client@6.5.0 --legacy-peer-deps
```

### 2. Generate schema

1. Prisma schema defines two models into direcotry `prisma`, each of which will map to a table in the underlying database: User and Post.
To actually create the tables in your database, you now can use the following command:
```bash
npx prisma db push
```
You should see following output:
![prisma-1](img/prisma1.png)





### 3.4.1. TODO

