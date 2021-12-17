---
layout: post
read_time: true
show_date: true
title:  How to deploy react app to GitHub pages
date:   2020-09-21 08:00:00 +0100
description: How to deploy react app to GitHub pages
img: posts/2020-09-21-DeployReactAppGithubPages/03_set_source_to_gh-pages.PNG
tags: [React, GithubPages]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/how-to-deploy-react-app-to-github-pages.html'
redirect_from:
  - /2020/09/21/how-to-deploy-react-app-to-github-pages.html
---

Github-pages is very practical to host static websites, not only Jekyll based websites, but also Angular, React based static websites etc.

You don't need to purchase a space for the websites hosting. It's totally free! All you need is just a GitHub account. :)

<!--more-->

Here are some steps you need to follow:

#### 1. Install Node.js if it's not already done

<br/>

#### 2. Create a react app with create-react-app CLI

```bash
> npx create-react-app my-app
```

<br />

#### 3. Configure the project's **package.json** file.

- Add a homepage url:

```javascript
"homepage": "https://{github_user_name}.github.io/{repository_name}",
```

![](./../../../assets/img/posts/2020-09-21-DeployReactAppGithubPages/01_homepage.png)

- Add **predeploy** and **deploy** steps

```javascript
    "scripts": {
        "predeploy": "npm run build",
        "deploy": "gh-pages -d build",
        ...
    }
```

<br />

#### 4. Create gh-pages branch in GitHub repository

![](./../../../assets/img/posts/2020-09-21-DeployReactAppGithubPages/02_create_gh-pages_branch.PNG)

Go to the **Settings** tab in the repository, and set the **gh-pages** branch as source.

![](./../../../assets/img/posts/2020-09-21-DeployReactAppGithubPages/03_set_source_to_gh-pages.PNG)

<br />

#### 5. Deploy React App to Github pages

Run **npm run deploy** to deploy React App to the repository.

```javascript
PROJECT_PATH>npm run deploy

> demo@0.1.0 predeploy PROJECT_PATH\demo
> npm run build


> demo@0.1.0 build PROJECT_PATH\demo
> craco build

Creating an optimized production build...
Compiled successfully.

File sizes after gzip:

401.16 KB (+4 B)  build\\static\\js\\31.68e127aa.chunk.js
340.96 KB         build\static\js\4.6285aef3.chunk.js
273.32 KB         build\static\js\2.a666de83.chunk.js
226.17 KB         build\static\js\35.aadd7357.chunk.js
...
112.58 KB         build\static\js\32.d0cc55a1.chunk.js
52.72 KB          build\static\css\31.aef428f6.chunk.css
50 KB             build\static\js\34.4e2843ba.chunk.js

The project was built assuming it is hosted at /GITHUB_REPOSITORY_NAME/.
You can control this with the homepage field in your package.json.

The build folder is ready to be deployed.

Find out more about deployment here:

bit.ly/CRA-deploy

> demo@0.1.0 deploy PROJECT_PATH\demo
> gh-pages -d build

Published
```

Congratulations! You have successfully deployed your React App to GitHub pages!
