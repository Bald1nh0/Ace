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
