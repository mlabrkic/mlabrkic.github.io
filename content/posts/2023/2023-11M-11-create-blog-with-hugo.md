---
title: "Create Blog With Hugo"
date: 2023-11-11T14:10:12+01:00
draft: false
categories:
- Development
tags:
- Blog
- Hugo
toc: true
---


------------------------------------------------------------
## 1 Quick start

gohugo: [Quick start](https://gohugo.io/getting-started/quick-start/)

Learn to create a Hugo site in minutes.

In this tutorial you will:\
1.1 Create a site\
1.2 Add content\
1.3 Configure the site


------------------------------
### Prerequisites

Before you begin this tutorial you must:

1. [Install Hugo](https://gohugo.io/installation/windows/#prebuilt-binaries) (==> hugo_extended_0.120.4_windows-amd64.zip)

`hugo version`\
==> v0.120.4

See: https://gohugo.io/commands/ and\
hugo help


2. [Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

`git --version`\
`git --help`

You must also be comfortable working from the command line.

/ gohugo: [Basic usage](https://gohugo.io/getting-started/usage/) /


------------------------------

### Step 1.1 Create a site

Run these commands to create a "Hugo site" with the Anatole theme.


(Windows Command Shell)

0) `cd C:\MY_GITHUB`

1) Create the [directory structure](https://gohugo.io/getting-started/directory-structure) for your project in the "mywebsite" directory.\
`hugo new site mywebsite --format yaml`\
==> hugo.yaml

See: https://gohugo.io/commands/hugo_new_site/ and\
hugo new site -h\
(hugo new site mywebsite  ==> hugo.toml)

2) Change the current directory to the root of your project.\
`cd mywebsite`

3) Initialize an empty Git repository in the current directory.\
`git init`

4) Clone the [Anatole theme](https://github.com/lxndrblz/anatole) into the "themes" directory, adding it to your project as a Git submodule.

`git submodule add https://github.com/lxndrblz/anatole.git themes/anatole`

5) Set the theme in your "hugo.yaml" to Anatole.\
`theme: anatole`


"hugo.yaml":

```yaml
baseURL: http://example.org/
languageCode: en-us
title: My New Hugo Site
theme: anatole
```


------------------------------

### Step 1.2 Add content

6) Add a new page to your site:\
`hugo new content posts/2023/2023-08M-23-windows-terminal.md`

See: https://gohugo.io/commands/hugo_new_content/ and\
hugo new content -h

Hugo created the file in the "content/posts" directory.

Open the file with your editor.

```
---
title: "Windows Terminal"
date: 2023-08-23T12:58:55+02:00
draft: true
---
```

Add some markdown to the body of the post.

---

7) Save the file, then start Hugo’s development server to view the site.
You can run either of the following commands to include "draft" content.

`hugo server --buildDrafts`\
`hugo server -D`

View your site at the URL displayed in your terminal.\
==> http://localhost:1313\
Keep the development server running as you continue to add and change content.\
Press Ctrl + C to stop Hugo’s development server.


When you finish editing the markdown document, you should set the "draft" value to "false".

2023-08M-23-windows-terminal.md

```
---
title: "Windows Terminal"
date: 2023-08-23T12:58:55+02:00
draft: false
categories:
- Utility
tags:
- Windows
- Windows Terminal
toc: true
---

## How to use the command palette in Windows Terminal

You can invoke the [command palette](https://learn.microsoft.com/en-us/windows/terminal/command-palette) by typing `Ctrl+Shift+P`.

...
```

Start Hugo’s development server to view the site.

`hugo server`\
==> http://localhost:1313


------------------------------

### Step 1.3 Configure the site

8) With your editor,
open the site configuration file (hugo.yaml or hugo.toml) in the root of your project.

* Set the baseURL for your production site.\
This value must begin with the protocol and end with a slash, as shown above.

* Set the languageCode to your language and region.
* Set the title for your production site.

"hugo.yaml":

```yaml
baseURL: https://mlabrkic.github.io/
languageCode: en-us  # Update to "en-gb" if you prefer, or another language!
title: Website of mlabrkic
theme: anatole
```


<details>
<summary>hugo.yaml - next step</summary>

```yaml
# themes\anatole\exampleSite\config\_default\config.toml
# https://gohugo.io/getting-started/configuration/

baseURL: https://mlabrkic.github.io/
languageCode: en-us  # Update to "en-gb" if you prefer, or another language!
title: Website of mlabrkic
theme: anatole

# summarylength: 10
enableEmoji: true

# https://github.com/lxndrblz/anatole/wiki
# Please note that the title under the [params] only adjusts the page title in the sidebar.
params:
  title: My website!
  author: mlabrkic
  description: Actually, this is the place for my notes!
  profilePicture: images/my_github_logo.jpg

  readMore: true
  copyright: 2023-{{ YEAR }} mlabrkic - Powered by [Hugo](https://gohugo.io/getting-started/quick-start/) & [Anatole](https://github.com/lxndrblz/anatole/wiki/)
  contentratio: 0.8
  # hidesidebar: true

  # Social links
  # use 'fab' when brand icons, use 'fas' when standard solid icons.
  socialIcons:
  - name: e-mail
    icon: "fas fa-envelope"
    title: "e-mail"
    url: "mailto:mlabrkic@hotmail.com"

  - name: Linkedin
    icon: "fab fa-linkedin"
    title: "Linkedin"
    url: "https://www.linkedin.com/in/mlabrkic/"

  - name: GitHub
    icon: "fab fa-github"
    title: "GitHub"
    url: "https://github.com/mlabrkic"

# https://gohugo.io/content-management/menus/#define-in-site-configuration
menu:
  main:
  - name: Home
    identifier: home
    weight: 100
    url: "/"

  - name: Archive
    identifier: posts
    weight: 200
    url: "/posts/"

  - name: Tags
    identifier: tags
    weight: 300
    url: "/tags/"

  - name: Categories
    identifier: categories
    weight: 400
    url: "/categories/"

```

</details>



<details>
<summary>hugo.yaml (+ markup  => my final configuration)</summary>

```yaml
# themes\anatole\exampleSite\config\_default\config.toml
# https://gohugo.io/getting-started/configuration/

baseURL: https://mlabrkic.github.io/
languageCode: en-us  # Update to "en-gb" if you prefer, or another language!
title: Website of mlabrkic
theme: anatole

# summarylength: 10
enableEmoji: true

# https://github.com/lxndrblz/anatole/wiki
# Please note that the title under the [params] only adjusts the page title in the sidebar.
params:
  title: My website!
  author: mlabrkic
  description: Actually, this is the place for my notes!
  profilePicture: images/my_github_logo.jpg

  readMore: true
  copyright: 2023-{{ YEAR }} mlabrkic - Powered by [Hugo](https://gohugo.io/getting-started/quick-start/) & [Anatole](https://github.com/lxndrblz/anatole/wiki/)
  contentratio: 0.8
  # hidesidebar: true

  # Social links
  # use 'fab' when brand icons, use 'fas' when standard solid icons.
  socialIcons:
  - name: e-mail
    icon: "fas fa-envelope"
    title: "e-mail"
    url: "mailto:mlabrkic@hotmail.com"

  - name: Linkedin
    icon: "fab fa-linkedin"
    title: "Linkedin"
    url: "https://www.linkedin.com/in/mlabrkic/"

  - name: GitHub
    icon: "fab fa-github"
    title: "GitHub"
    url: "https://github.com/mlabrkic"

# https://gohugo.io/content-management/menus/#define-in-site-configuration
menu:
  main:
  - name: Home
    identifier: home
    weight: 100
    url: "/"

  - name: Archive
    identifier: posts
    weight: 200
    url: "/posts/"

  - name: Tags
    identifier: tags
    weight: 300
    url: "/tags/"

  - name: Categories
    identifier: categories
    weight: 400
    url: "/categories/"

# https://gohugo.io/getting-started/configuration-markup/#goldmark
# https://gohugo.io/getting-started/configuration-markup/#highlight
markup:
  goldmark:
    renderer:
      unsafe: true
  highlight:
    # style: monokai
    # style: perldoc  (No, because of bad rendering of the yaml code on the smartphone!!!)
    style: solarized-light

```

</details>
<br>

Anatole theme Wiki: [Anatole theme documentation](https://github.com/lxndrblz/anatole/wiki)

Because it can happen that the author of "Anatole theme" deletes its repo, backup the Anatole theme locally to your HDD.


------------------------------------------------------------

## 2 Host on GitHub Pages

gohugo: [Host on GitHub Pages](https://gohugo.io/hosting-and-deployment/hosting-on-github/)\
Deploy Hugo as a GitHub Pages project or "personal/organizational" site
and automate the whole process with GitHub Actions.

Prerequisites:  Create a Hugo site and test it locally with "hugo server".

------------------------------
#### Step 2.1 Create a GitHub repository (public)

GitHub: [Create a repo](https://docs.github.com/en/get-started/quickstart/create-a-repo)

> **NOTE:**
To avoid errors, leave this repo empty (no: README.md, LICENSE, .gitignore files (or workflow yml))!!!\
(See below:  Adding a local repository to GitHub using Git)

Repository name: `mlabrkic.github.io`\
https://github.com/mlabrkic/mlabrkic.github.io


------------------------------
#### Step 2.2 Push your local repository to GitHub

GitHub: [Adding a local repository to GitHub using Git](https://docs.github.com/en/migrations/importing-source-code/using-the-command-line-to-import-source-code/adding-locally-hosted-code-to-github#adding-a-local-repository-to-github-using-git)

```
Change the current working directory to your local project:
cd mywebsite

(git remote add origin https://github.com/mlabrkic/mlabrkic.github.io.git)
(git remote remove origin)
==>
git remote add origin https://mlabrkic:GPAT@github.com/mlabrkic/mlabrkic.github.io.git

To list the remote repositories that are configured, along with their URLs:
git remote -v

git status

If "master" branch was initially created, and I want to change its name to "main":
git branch -M main

git add .
git commit -m "Initial setup of website"

To push the changes in your local repository to GitHub.com, run the following command.
git push origin main
```

GPAT = Personal access token

GitHub: [Creating a personal access token (classic)](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#creating-a-personal-access-token-classic)


------------------------------
#### Step 2.3 Visit your GitHub repository

1. On GitHub, navigate to your "site's repository".
2. Under your repository name, click "Settings".
3. In the "Code and automation" section of the sidebar, click "Pages".
4. Under "Build and deployment", under "Source", you will see this: "Deploy from a branch".


------------------------------
#### Step 2.4 Change the Source to "GitHub Actions"

GitHub: [Publishing with a custom GitHub Actions workflow](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-with-a-custom-github-actions-workflow)

Change the Source to "GitHub Actions".\
The change is immediate; you do not have to press a Save button.

Use a suggested workflow, "browse all workflows", or create your own.


------------------------------
#### Step 2.5 Use Hugo workflow from GitHub "starter workflows"!

**NOTE:**
GitHub will suggest several [starter workflows](https://github.com/actions/starter-workflows/tree/main/pages).\
If you already have a workflow to publish your site, you can skip "Step 2.5" and go to "Step 2.6".

"browse all workflows" ==> Choose a workflow

Search: hugo, enter\
==> Found 1 workflow\
Hugo, By GitHub Actions

Click "Configure"!

**Edit**:

1. Rename: hugo.yml  ==>  gh-pages.yml
2. branches: ["main"]
3. HUGO_VERSION: 0.120.4

4. Comment these 2 lines:

```yaml
- name: Install Dart Sass
  run: sudo snap install dart-sass
```

(You may remove this step if your site, themes, and modules
do not transpile Sass to CSS using the Dart Sass transpiler.)


GitHub: [Commit your first change](https://docs.github.com/en/get-started/quickstart/create-a-repo#commit-your-first-change)

Preview:

Click "Commit changes"!
==>
to the main branch

The GitHub Pages settings "will link to the workflow run"
that "most recently deployed your site".


------------------------------
#### Step 2.6 Use your Hugo workflow!

Create a new folder in your local repository:\
.github/workflows/

Find hugo.yml somewhere, or download\
https://github.com/actions/starter-workflows/blob/main/pages/hugo.yml\
In fact, this is the same Hugo workflow above (from GitHub starter workflows)!

Copy it to the .github/workflows/ folder.

**Edit**:
Everything the same as in "Step 2.5" (1 - 4).


------------------------------
#### Step 2.7 Commit the change to your local repository

Commit the change to your local repository with a commit message of something like "Add workflow", and push to GitHub.

```
(git pull origin main)

git status
git add .
git commit -m "Add workflow"

To push the changes in your local repository to GitHub.com, run the following command.
git push
```

------------------------------
#### (Step 2.8 and Step 2.9) From GitHub's main menu, choose Actions

You will see something like this:

1 workflow run
"Add workflow"

When GitHub has finished building and deploying your site,
the color of the status indicator will change to green.

------------------------------
#### Step 2.10 Click on the commit message as shown above

You will see this:

gh-pages.yml\
build ==> deploy

Under the deploy step, you will see a link to your live site.\
https://mlabrkic.github.io/

In the future, whenever you push a change from your local repository,
GitHub will rebuild your site and deploy the changes.


------------------------------------------------------------
#### References:

* sgibson91: [Blogging with Hugo and GitHub Pages](https://carpentries-incubator.github.io/blogging-with-hugo-and-github-pages/)\
(Attention, here the GitHub website repo is first created, then copied to the local HDD, and then the Hugo site is created.)

* GitHub: [Getting started with GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages)
* GitHub: [Learn GitHub Actions](https://docs.github.com/en/actions/learn-github-actions)

* GitHub Pages: [Custom GitHub Actions Workflows (beta), July 27, 2022](https://github.blog/changelog/2022-07-27-github-pages-custom-github-actions-workflows-beta/)

* GitHub Pages: [GitHub Pages now uses Actions by default, August 10, 2022](https://github.blog/2022-08-10-github-pages-now-uses-actions-by-default/)






