---
title: "My experience with Hugo"
date: 2022-07-31T17:15:07+03:00
# draft: true
---

This is my certificate of completion the course [Learning Static Site Building with Hugo](https://epa.ms/1XSG2):

![Hugo sertificate](/img/certificate.png)

A static site generator (SSG) is a tool that generates a full static HTML website based on the plain text documents written in Markdown or other lightweight markup language and a set of templates. See more details on what is [SSG](https://www.cloudflare.com/learning/performance/static-site-generator/).

Also, see my short user guide on how to create a static website using **Hugo**, based on the course above.

**Prerequisites**:
- You're have installed and familiar with any source-code editor like [Visual Studio Code](https://code.visualstudio.com).
- You know how to run commands using a CLI like Command Prompt/Windows PowerShell.
- You have [Git installed](https://git-scm.com/download/win) and familiar with [Git commands](https://docs.github.com/en/get-started/using-git/about-git#basic-git-commands). To check if Git is installed, run `git --version` in CLI.
- You know the syntax of [Markdown](https://www.markdownguide.org/basic-syntax).
- You have account in [GitHub](https://github.com/Dmytro-Kozachok?tab=repositories).

**User guide**:
1. [Install Hugo](https://gohugo.io/getting-started/installing), then check it in the CLI:

```sh
hugo version
```

2. Create your website locally in a dedicated Hugo folder on your local machine, e.g., **Sites**, which should be separated from the installation Hugo folder, e.g., **bin**. Go to this folder in your CLI:

```   
  cd C:\hugo\sites
  hugo new site <your_site_name>
  cd .\<your_site_name>
```

3. Initiate your local Git repository for the site, check the list of untracked files, copy all the folders into the local Git repository, and commit these to Git:

```sh
  git init
  git status
  git add --all
  git commit -m "<Commit_message>"
```

4. Place link of a selected [Hugo theme](https://themes.gohugo.io), e.g. **minimalist**, into the **themes** root folder:

```sh
  cd themes
  git submodule add https://<github_theme> themes/<theme_name>
```

5. Copy the **themes > theme_name > config.toml** file's content into the **config.toml** root file and then adjust the required file properties there:

    ![config-toml](/img/config-toml.png)

    For a Hugo theme with the localization file in place, e.g., **l10n.toml** for **minimalist** theme, copy this file from **themes > theme_name > exampleSite > data** folder into the **data** root project folder. Also, don't forget to delete `themesDir` property in your **config.toml** root file to be able to launch your site locally:
    
    ![themeDir](/img/l10n-themeDir.png)

    Commit the changes:

```sh
  git add --all
  git commit -m "<Commit_message>"
```

6. Run your site on a local server [localhost:1313](http://localhost:1313/):

```sh
  hugo server
```

7. Create a new webpage on the **content** root project folder, or a new post on the **content > post** folder (e.g., the last is applicable for blog-based Hugo themes like **minimalist**):

```sh
  hugo new <site_page_name>.md
  hugo new post/<site_post_name>.md
```

8. Create **static > img** folder, copy required images there and update uploaded image names in **config.toml** root project file (recommendation -- check **Disable cache** box in the **Network** tab of the browser dev panel to avoid the image caching).

9. Build your site:

```sh
  hugo
```

10. Create **.gitignore** root file and enter `public/` property there (to make Git ignore the content of the **public** root project folder):

  ```sh
  git add .gitignore
  git commit -m "<Commit_message>"
  ```

11. Create your Hugo project repository in GitHub and push the master branch from your local Git repository there:

```sh
 git remote add origin https://<your_hithub_repo>
 git push -u origin master 
 ```

12. Sign in to [Travis CI](https://app.travis-ci.com/account/repositories) with your GitHub account and sync your repo there.

13. Create **.travis.yml** root project file with the script to allow Travis CI to build your site:

```sh
  install:
  - wget https://<latest_github_hugo_linux_release>
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

14. Commit and push the Travis' support script to Git (Travis will run the script automatically to build your site afterwards. If not, restart the build manually on your project page in Travis):

```sh
  git add --all
  git commit -m "<Commit_message>"
  git push origin
```

15. (optional) Get a domain name for your site to public it on the Internet, e.g., using [Namecheap](https://www.namecheap.com/).

16. Sign in to [Netlify](https://app.netlify.com/sites/dmytryko/overview) with your GitHub account, then deploy and name your site following the inline instructions.

17. Check out your website on the Internet by the Netlify link generated in the format **<your_site_name>.netlify.app**, e.g., https://dmytryko.netlify.app.