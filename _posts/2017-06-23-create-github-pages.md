---
layout: post
title:  "How to create github pages"
project: false
---

Step by step process to create github pages

## Create personal github pages
1. Select a github pages theme. For starters, here are some sources:
```
https://pages.github.com/themes/
https://drjekyllthemes.github.io/
```
- If you want to re-use reference portfolio format. Go to Step 2
-  *Note: If you dont want to go through the trouble of changing the html layout or to add pictured, then choose a theme that already satisfies your requirement. So, prioritize accordingly*

2. Find the pages theme on github and get the repo link. 
- This is the reference repo link:
```
https://github.com/ByronAllen/ByronAllen.github.io
```

3. Once on the github reference page: Fork it!

4. Naming the forked folder: Go to the Settings icon in your personal forked or newly created github repo.
- Name of the repo : <yourgithubname>.github.io
- Ensure the name is exactly the as your github repo name

5. Scroll down on the setting page. You will see a link to your portfolio page https://<yourgithubname>.github.io/

**The contents are still from the reference profile. Remember to delete the reference posts if you dont want his posts to be visible on your profile**

## Change the contents
1. Config.yml file is the face of your blog. Change your Name, email id, linkedin and github usernames in this file.

2. about.md - This has the content of your About page in your page

3. /_posts/ - This folder contains the posts that are displayed in your Portfolio page.

- These are markdown files. That is the format we used to write Markdown content in our Jupyter notebook.
- The naming convention of the post that is recognised by this template is:  <YYYY-MM-DD-name-of-post>.md
- Refer to a .md file from the reference portfolio to 

4. /images/ - This folder can be used to put images to be displayed in your posts.

gem install github-pages


