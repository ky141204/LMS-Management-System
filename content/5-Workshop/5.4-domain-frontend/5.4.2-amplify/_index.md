---
title: "Deploy the Frontend with Amplify"
date: 2026-07-01
weight: 2
chapter: false
pre: " <b> 5.4.2. </b> "
---

<div class="lms">

# Deploy the web frontend with AWS Amplify

Deploy the frontend (React/Vite) from GitHub to AWS Amplify.

**Open the AWS Amplify service.**
![Navigate to AWS Amplify](images/Screenshot%202026-07-09%20230957.png)

**Choose GitHub as the source provider and grant access.**
![Choose GitHub as the source provider](images/Screenshot%202026-07-09%20231022.png)

**Choose the `LMS_System_MongoDB` repository, branch `main`, enable monorepo, and set the root directory to `frontend`.**
![Choose repository, branch, and monorepo directory](images/Screenshot%202026-07-09%20231056.png)

**Configure the build: command `npm run build`, output directory `dist`.**
![Configure the application build](images/Screenshot%202026-07-09%20231113.png)

**Add the environment variable `VITE_BACKEND_URL = https://api.fixing404.win/api` so the frontend can call the backend.**
![Add the VITE_BACKEND_URL environment variable](images/Screenshot%202026-07-09%20231228.png)

**Review the repository and branch configuration.**
![Review configuration (1)](images/Screenshot%202026-07-09%20231239.png)

**Review the advanced configuration and environment variables, then choose Save and deploy.**
![Review configuration (2)](images/Screenshot%202026-07-09%20231245.png)

**Deployment succeeds, and the application runs on an `*.amplifyapp.com` domain.**
![Application deployed successfully on Amplify](images/Screenshot%202026-07-09%20231300.png)

</div>
