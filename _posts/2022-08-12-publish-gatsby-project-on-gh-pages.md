---
layout: article
title: "Publish a Gatsby project on github pages"
excerpt: "Host your static site for free on github pages!"
date: 2022-08-03 
tags: [Gatsby, Github pages]
mathjax: false
mathjax_autoNumber: false
key: publish-gatsby-site-on-github-pages
---

<div align="center">
  <img src="https://raw.githubusercontent.com/is-this-echo/blog-img-hosting/main/images/gatsby-logo.png" alt="Gatsby logo" width="8%">
</div>


- [ ]  Create the project on local machine.
- [ ]  Install github pages npm package as a dev dependency in the project.

```jsx
npm i gh-pages --save-dev
```

- [ ]  Modify package.json in the project root directory to include a deploy script command under scripts tag.

```jsx
"scripts" : {
	"deploy" : "gatsby build --prefix-paths && gh-pages -d public",
	......
}
```

- [ ]  Modify gatsby-config.js to include “pathPrefix” in the exports.

```jsx
module.exports = {
	pathPrefix : "/<repository-name>",
	.....
}
```

- [ ]  Run the deploy script.

```jsx
npm run deploy
```

- [ ]  Commit the code and push to remote .

```jsx
git add *
git commit -am "first publish"
git push origin main
```

At this point, a new branch **gh-pages** will be created in the remote repo. 

<div align="center">
  <img src="https://raw.githubusercontent.com/is-this-echo/blog-img-hosting/main/images/gatsby-gh-page1.png" alt="github pages branch" width="50%">
</div>

- [ ]  Go to the repo on github, then `Settings`→`Pages` (left sidebar). It will open up the config settings for github pages.
Now, for the **Source**, select Deploy from branch  from the dropdown. **Branch** → gh-pages from the dropdown and select root 📂 , then hit save.

<div align="center">
  <img src="https://raw.githubusercontent.com/is-this-echo/blog-img-hosting/main/images/gatsby-gh-page2.png" alt="github pages deploy" width="100%">
</div>
After all these steps are done, the static site will be hosted on github pages, the deployment can be checked on _https://github-username.github.io/repository-name_

---
If you like TeXt, don't forget to give me a star. :star2:

[![Star This Project](https://img.shields.io/github/stars/is-this-echo/is-this-echo.github.io.svg?label=Stars&style=social)](https://github.com/is-this-echo/is-this-echo.github.io)