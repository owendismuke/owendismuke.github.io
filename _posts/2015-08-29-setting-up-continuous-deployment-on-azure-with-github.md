---
layout: post
title:  "Using GitHub for Continuous Deployment to Azure"
date:   2015-08-29 14:00:49-7
categories:
- Azure
- GitHub
- deployment
comments: true
---

*Note: This article assumes you already have an account with Azure, a Web App created, and a GitHub repository just waiting to deploy.*

[Microsoft Azure][azure] is a create place to quickly host your web application for the world to see. [GitHub][gh] is a great place to store, collaborate on, and version control your code base. Wouldn't it be great if they could just talk to each other and deploy your new code whenever you pushed it to [GitHub][gh]? It just so happens that they can.

### Step 1:  
Get all of your code working and push it to your [GitHub][gh] repository. You will want to choose which branch to use as the deployed branch and remember this for later.

### Step 2:  
Log in to your Azure account and bring up the Web App you created for this project.

### Step 3:  
Connect Azure to your GitHub repository. Depending on if you are using the preview or classic portal on Azure, the steps will be different.

#### Azure Preview Portal:  
+  In `Settings > Continuous Deployment > Choose Source`, select GitHub.
+  If this is your first time connecting to GitHub, enter your credentials and grant access to the necessary organizations.
+  Choose the organization that the repository belongs to.
+  Choose the project (repository).
+  Choose the deployment branch you made note of earlier.
+  Fix any errors and enjoy your deployed site.

#### Azure Portal (classic):  
+ In the Dashboard, select `Set up deployment from source control` from the quick glance menu on the right under the graph.
+ Select GitHub from the options given in `Where is your source code?`  and click the right arrow at the bottom of the pop up.
+ If this is your first time connecting to GitHub, enter your credentials and grant access to the necessary organizations.
+ Select the repository from the dropdown menu and manually enter the name of the branch to deploy in the input box.
+ Fix any errors and enjoy your deployed site.


[azure]: http://azure.microsoft.com
[gh]: http://www.github.com