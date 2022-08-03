---
title: "My experience with Hugo"
date: 2022-07-31T17:15:07+03:00
# draft: true
---

This is my certificate of completion the course [Learning Static Site Building with Hugo](https://epa.ms/1XSG2):

![Hugo sertificate](/img/certificate.png)

Based on this course, this short user guide explains how to create a static website using [**Hugo**](https://gohugo.io/) SSG.

**Prerequisites**:
- You have at least basic understanding of what is a [static site generator (SSG)](https://www.cloudflare.com/learning/performance/static-site-generator/) and the [docs-as-code approach](https://docsy-site.netlify.app/docs/static-site-generators/docs-as-code/#docs-as-code).
- You have installed and familiar with any source-code editor like [Visual Studio Code](https://code.visualstudio.com).
- You're familiar with Command Line Interface (CLI) like Command Prompt or Windows PowerShell.
- You're familiar with [Git commands](https://docs.github.com/en/get-started/using-git/about-git#basic-git-commands) and have Git installed on your local machine. If not, [install Git](https://git-scm.com/download/win) and check it in the CLI by running **`git --version`**.
- You know the syntax of [Markdown](https://www.markdownguide.org/basic-syntax).
- You have account in [GitHub](https://github.com/).

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

4. Place link of a selected [Hugo theme](https://themes.gohugo.io) into the **themes** root folder:

```sh
  cd themes
  git submodule add https://<github_theme> themes/<theme_name>
```

5. Copy the **themes > theme_name > config.toml** file content into the **config.toml** root file and then adjust there the required file properties:

    ![config-toml](/img/config-toml.png)

    For a Hugo theme with the localization file in place, e.g., **l10n.toml** for **minimalist** theme, copy this file from **themes > theme_name > exampleSite > data** folder into the **data** root project folder. Also, don't forget to delete **`themesDir`** property in your **config.toml** root file to be able to launch your site locally:
    
    ![themeDir](/img/l10n-themeDir.png)

    Commit the changes:

```sh
  git add --all
  git commit -m "<Commit_message>"
```

6. Run your site on the local server [localhost:1313](http://localhost:1313/):

```sh
  hugo server
```

7. Create a new page under the **content** root folder, or a new post under the **content > post** folder (e.g., posts are applicable for the blog-based Hugo themes like **minimalist**):

```sh
  hugo new <site_page_name>.md
  hugo new post/<site_post_name>.md
```

8. Create the **static > img** folder, place all required images there and update uploaded image-related properties in the **config.toml** root file. Recommendation: check the **Disable cache** box in the **Network** tab of your browser's dev panel to avoid possible image caching.

9. Build your site:

```sh
  hugo
```

10. Create the **.gitignore** root file and enter the **`public/`** property there (to make Git ignore the content of the **public** root project folder):

  ```sh
  git add .gitignore
  git commit -m "<Commit_message>"
  ```

11. Create a [GitHub repository](https://github.com/new/) for your Hugo project and push there the master branch from your local Git repository:

```sh
 git remote add origin https://<your_hithub_repository>
 git push -u origin master 
 ```

12. Sign in to [Travis CI](https://app.travis-ci.com/account/repositories) with your GitHub account and sync your repository there.

13. Create the **.travis.yml** root file in your project with the script below to allow Travis CI to build your site each time you commit and push updates for your site:

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

14. Commit and push the Travis script to Git -- Travis will run the script automatically to build your site. If that didn't happen, start the build manually on your project page in Travis:

```sh
  git add --all
  git commit -m "<Commit_message>"
  git push origin
```

15. (optional) Get a domain name for your site to public it on the Internet, e.g., using [Namecheap](https://www.namecheap.com/).

16. Sign in to [Netlify](https://app.netlify.com/sites/dmytryko/overview) with your GitHub account, then deploy and name your site following the inline instructions. For more details, refer to the [publish via Netlify](https://docsy-site.netlify.app/docs/static-site-generators/jekyll/#publish-your-site) article of my teammate Ivan Cheban.

17. Check out your website on the Internet by the Netlify link generated in the format _<your_site_name>.netlify.app_, e.g., https://dmytryko.netlify.app.

---
**And last but not least!**

Each time you make any updates to your site, don't forget to apply them by sequential running these commands in the CLI:
```sh
  git add --all
  git commit -m "<Commit_message>"
  git push origin
```
---