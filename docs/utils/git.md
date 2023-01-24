---
title: Overview Git
summary: 
authors:
    - Paul van Genuchten
    - Luís Moreira de Sousa
date: 2023-01-06
---

# Overview Git

Git is a distributed version management system of mainly text files to facilitate shared development of software and/or documentation. Git is one of the creations of Linus Torvalds. In Git everybody `checks out` the full repository with all its history, you make changes to a version locally and `push` them back to the server. In the process incidental `conflicts` may occur, if someone else has made a change in the same version and line as you. The server will reject the push until you resolved the conflict.

Git is mainly operated from the command line, but a lot of client software is available to facilitate participation. An example is [SmartGit](https://www.syntevo.com/smartgit/), which provides an easy to use interface to manage even complex git tasks such as fixing conflicts. [Git GUI](https://github.com/prati0100/git-gui/) is the graphical user interface included with the Git software suite.

[GitHub.com](https://github.com) is a well known provider of Git services. They offer a lot of additional functionality on top of the Git version management, such as a web interface, issue management, forking & pull requests, wiki, actions, etc.

[Gitlab](https://about.gitlab.com/) is a popular open source software stack offering a similar set of functionality as GitHub, you can use it as [SAAS](https://en.wikipedia.org/wiki/Software_as_a_service) or install it on a server.

In 2020 various code forges based in the United States arbitrary blocked access
to users from countries deemed hostile. This action affected foreign students
and scientists working in Europe or collaborating with European institutions.
That same year a community of European software developers registered a
non-for-profit in Germany to support an independent code forge hosted in Europe.
The result is [Codeberg](https://codeberg.org/), a free, open source, Git-based
code forge accessible to everyone in the world.

An interesting [quick start to Git](https://rogerdudler.github.io/git-guide/) is written by Roger Dudler (multiple translations). Or if you [prefer a video](https://git-scm.com/video/what-is-git).

The main reference for this software is the [Git Book](https://git-scm.com/book/en/v2).

## Git Use Cases

- A software project with contributors from around the globe. Including issue management, software releases and automated validation of unit and integration tests.
- This wiki is maintained in a Git repository. With every new push a new version is build and it replaces the previous version.
- A roll out of an improved composition of Docker containers on a cloud platform like [Kubernetes](https://kubernetes.io/). The helm charts (configuration files) are stored on a Git repository, every change to the helm chart results in an update of the development environment to reflect the latest changes.
- Git is an important tool for Dev Ops staff. Manual interventions are minimized. Every action is scripted, stored in a Git repository and started from a Git action. This improves tracebility and reproducability in software maintenance.

## Exersize

- Install [git](https://git-scm.com/download/) (or smartgit, which has git included) on your machine 
- Clone the repository of this wiki from the command line:

```
git clone https://github.com/ejpsoil/soildata-assimilation-guidance.git
```

- open the folder and log all events that happened on the repository 

```
cd soildata-assimilation-guidance
git log --oneline
```

## Forking and Pull requests 

GitHub added an extra interactivity on top of Git, the option to `Fork` a repository to a personal space. And from the personal space provide an option to propose a change to the `upstream` repository, this is called a `pull request`. Now users were able to propose changes to repositories of which they were not even a member yet. The fork and pull mechanism has now been adopted by other git platforms, such as Gitlab, but because it is not part of the Git specification itself, it may work slightly different on other platforms. Let's try and improve this wiki via a pull request:

- If you do not have a github account yet, we invite you to set up one now at https://github.com/signup.
- When logged in, open https://github.com/ejpsoil/soildata-assimilation-guidance, and click the fork button in the top right. This will clone the repo to your personal space.
- On https://github.com/*YOU*/soildata-assimilation-guidance, edit a file (maybe you found a typo somewhere, or would like to comment/extend something) via the github web interface by opening the file and clicking on the pencil button.
- Below the text you notice a commit message and button. Every commit in Git requires a usefull message, so others understand what you did. Select the option "Create a new branch for this commit ...".
- Then create the branch, but not the pull request in the next step, because this pull request would arrive in your own repository
- Now navigate back to https://github.com/ejpsoil/soildata-assimilation-guidance. A banner shows indicating you can `compare and pull request` your recent change. Click this button and create the pull request.

The process of a pull request is quite overwhelming. But it is an important aspect in collaborative development these days. Many repositories only allow code changes via pull requests, because it is a guarantee that at least 2 persons have looked at it.
