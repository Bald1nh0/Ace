# Ace
### Test task:
1. Organize infrastructure  
- A web project with 1 page: index.html;
- There is a public GitHub repository;
- There are 3 branches: dev, staging, prod;
- The index.html page is hosted on Firebase;
- There are 2 accounts in Firebase: 1st - for staging, 2nd - for production;
- There is also a Slack chat. Slack has a separate channel for CI|CD events;
2. Events
- Every time anyone pushes to staging, you need to automatically organize the upload of index.html to the staging firebase server. After that, you need send a message to the slack channel that this happened, with a link to the address where you can view the result;
- Every time anyone pushes to prod, you need to automatically organize uploading index.html to the production firebase server. After that,you need to send a message to the slack channel that this happened, with a link to the address where you can view the result;
---
[URL of staging server](https://stage-c294c.web.app/ "URL of staging server")  
[URL of production server](https://ace-123.web.app/ "URL of production server")  
The links to the projects are permanent and the content is updated after a successful deployment.

---

### My thoughts:
There is no need to make 2 servers separately for production and staging. We can deploy changes from the staging branch to the preview channel Firebase and:
- GitHub Action can create a new preview channel (and its associated preview URL) for every push or PR on your GitHub repository.
- Adds a comment to the PR with the preview URL so that you and each reviewer can view and test the PR's changes in a "preview" version of your app.
- Updates the preview URL with changes from each commit by automatically deploying to the associated preview channel. The URL doesn't change with each new commit.
- (Optional) Deploys the current state of your GitHub repo to your live channel when the PR is merged.
Reminder: When using preview URLs, your app interacts with the real backend resources of your Firebase project.  

[This is written in the firebase documentation](https://firebase.google.com/docs/hosting/github-integration?authuser=0 "Firebase documentation")  
For this we need to add a workflow in a staging branch (.github/workflows/deploy-preview.yml):    
      
    name: Deploy to Preview Channel  
    'on':
    push:
        branches:
        - staging
    jobs:
    build_and_preview:
        runs-on: ubuntu-latest
        steps:
        - uses: actions/checkout@v2
        - uses: FirebaseExtended/action-hosting-deploy@v0
            with:
            repoToken: '${{ secrets.GITHUB_TOKEN }}'
            firebaseServiceAccount: '${{ secrets.FIREBASE_SERVICE_ACCOUNT_STAGE_C294C }}'
            expires: 30d
            projectId: stage-c294c
