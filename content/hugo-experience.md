---
title: "My experience with Hugo"
date: 2022-07-31T17:15:07+03:00
# draft: true
---

This is my certificate of completion the course [Learning Static Site Building with Hugo](https://epa.ms/1XSG2):

![Hugo sertificate](/img/certificate.png)

Also, see my short user guide on how to create a static website using Hugo, which is based on the course above:

1. Install [Hugo](https://gohugo.io/getting-started/installing) and [Git](https://git-scm.com/download/win), then check in the Terminal/PowerShell if they're installed:

```
hugo version
git --version
```

2. Create your website template (e.g., **your-site-name**) in the site-related Hugo folder, e.g., **Sites**, which is separated from the installation-related Hugo folder **bin** (and switch to this folder afterwards):

```    
  cd C:\hugo\sites
  hugo new site your-site-name
  cd .\your-site-name
```

3. Initiate your local git repository for the site, (optionally) check the list of untracked files, copy all the folders into the local git repository, commit the action and push all the branches to the main one:

```
  git init
  git status
  git add --all
  git commit -m "Commit-message"
  git push origin
```

4. Copy GitHub link of the Hugo [theme](https://themes.gohugo.io) you've chosen into the **themes** root project folder:

```
  git submodule add https://github-theme-url themes/theme-name
```

5. Copy **themes > theme-name > config.toml** file's content into **config.toml** root folder and adjust required file properties, then commit this (for **minimalist** Hugo theme, copy **l10n.toml** file from **themes > theme-name > exampleSite > data**  to **data** root folder):

```
  git add --all
  git commit -m "Commit-message"
```

6. Build the site locally and then check it on the localhost which is generated once the command run:

```
  hugo server
```

7. Create a new webpage on the **content** root project folder; create a new post on the **content > post** folder (e.g., applicable for **minimalist** theme):

```
  hugo new site-page-name.md
  hugo new post/site-post-name.md
```

8. Create **static > img** folder, copy required images there and update uploaded image names in **config.toml** root project file (recommendation -- check **Disable cache** box in the **Network** tab of the browser dev panel).

9. Build your site:

```
  hugo
```

10. Create **.gitignore** root file and enter `public/` property there (to make Git ignore the content of the **public** root project folder):

  ```
  git add .gitignore
  git commit -m "Commit-message"
  ```

11. Create your Hugo project repository in [GitHub](https://github.com/Dmytro-Kozachok?tab=repositories) and push the master branch from your local Git repository there:

```
 git remote add origin https://your-hithub-repo-url
 git push -u origin master 
 ```

12. Sign in to [Travis CI](https://app.travis-ci.com/account/repositories) with your GitHub account and sync your repo there.

13. Create **.travis.yml** root project file with the script:

```
  install:
  - wget https://latest-github-hugo-linux-release-url
  - sudo dpkg -i hugo*.deb
  - hugo version
  before_script:
  - rm -rf public
  script:
  - hugo
  branches:
   only:
   - master
```

14. Commit and push the Travis' support activity to Git (Travis will run the script automatically to build your site afterwards):

```
  git add --all
  git commit -m "Commit-message"
  git push origin
```

15. (optional) Get a domain name for your site to public it on the Internet, e.g., using [Namecheap](https://www.namecheap.com/).

16. Sign in to [Netlify](https://app.netlify.com/sites/dmytryko/overview) with your GitHub account, then deploy and name your site following the inline instructions.

17. Check out your website on the Internet by the link generated in the format **your-site-name.netlify.app**, e.g., https://dmytryko.netlify.app.