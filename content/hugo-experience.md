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
- You use MS Windows 10/11 as your operating system
- You're familiar with any source-code editor like [Visual Studio Code](https://code.visualstudio.com/)
- You have installed a CLI like Command Prompt, Terminal, or Windows PowerShell
- You know markup format [Markdown](https://www.markdownguide.org/basic-syntax/), the most common documentation source format for docs-as-code
- You have basic understanding on how to use Git and GitHub

**User guide**:
1. Install [Hugo](https://gohugo.io/getting-started/installing) and [Git](https://git-scm.com/download/win), if it isn't installed on your local machine, then check in the CLI if they're installed:

```sh
hugo version
git --version
```

2. Create your website template named as **<your_site_name>** in the site-related Hugo folder, e.g., **Sites**, which should be separated from the installation Hugo folder, e.g., **bin**; open this folder in the Terminal/PowerShell:

```   
  cd C:\hugo\sites
  hugo new site <your_site_name>
  cd .\<your_site_name>
```

3. Initiate your local git repository for the site, check the list of untracked files, copy all the folders into the local git repository, and commit the action to Git:

```sh
  git init
  git status
  git add --all
  git commit -m "<Commit_message>"
```

4. Place the GitHub link of the Hugo [theme](https://themes.gohugo.io) you selected, e.g. **minimalist** theme, into the **themes** root project folder:

```sh
  cd themes
  git submodule add https://<github_theme> themes/<theme_name>
```

5. Copy the **themes > theme-name > config.toml** file's content into the **config.toml** root project file and then adjust the required file properties there:

    ![config-toml](/img/config-toml.png)

    For a Hugo theme with the localization file in place, e.g., **l10n.toml** for **minimalist** theme, copy this file from **themes > theme-name > exampleSite > data** folder into the **data** root project folder. Also, don't forget to delete `themesDir` property in your root project **config.toml** file to be able to launch your site locally:
    
    ![themeDir](/img/l10n-themeDir.png)

    Commit the changes:

```sh
  git add --all
  git commit -m "<Commit_message>"
```

6. Run your site on a local server [localhost](http://localhost:1313/):

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

11. Create your Hugo project repository in [GitHub](https://github.com/Dmytro-Kozachok?tab=repositories) and push the master branch from your local Git repository there:

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

17. Check out your website on the Internet by the link generated in the format **<your_site_name>.netlify.app**, e.g., https://dmytryko.netlify.app.