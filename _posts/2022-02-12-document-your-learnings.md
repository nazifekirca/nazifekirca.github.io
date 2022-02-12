---
layout: post
title: Effective journaling on your blog
subtitle: How to document your learning in markdown
categories: Markdown
tags: [Markdown, journaling, blog]
---

## Prerequisites

- If you haven't create a Jekyll blog page on Github yet, please follow [this tutorial](https://dev.to/teaberlin/build-an-awesome-website-for-free-59ho) to create your own free website.
- If you don't have a code editor yet, you won't make a mistake by picking VS Code. [Download](https://code.visualstudio.com/download) and install the version that is right for your operating system.
- If you haven't installed Git yet, install it on [Mac OS](https://www.atlassian.com/git/tutorials/install-git#mac-os-x), [Windows](https://www.atlassian.com/git/tutorials/install-git#windows) or [Linux](https://www.atlassian.com/git/tutorials/install-git#linux).
- Now you can [clone your Github repo](https://code.visualstudio.com/docs/editor/github) and edit it in VS Code. You'll love it!

## Create a post to document your learnings
### The right place

After opening your repository folder in VSCode, you will see the following file structure on the left side of your screen:

![folder_structure_in_VSCODE](/assets/images/post_images/document_your_learnings/folder_structure_in_VSCODE.png)

To create a new post, open the `_posts` folder and create a new file. 

### The right name

For your jekyll blog to recognize the new file as a blog post, it does not only have to be inside of the `_posts` folder, it also needs to follow the right naming convention:

> year-month-day-filename.md

The file you are currently looking at is called

> 2022-02-12-document-your-learnings.md

### The right header

Now that you named your file, you can open and edit it. As your first edit, you should pass the right header information. You can just copy and paste the following header (this is the header used in the post you're currently reading) to the top of your article and customize the values to your needs.

```
---
layout: post
title: Effective journaling on your blog
subtitle: How to document your learning in markdown
categories: Markdown
tags: [Markdown, journaling, blog]
---
```

Quick explanation of the attributes:

1. `layout`: defines which layout will be applied to this file when being rendered. This needs to be set to **post**
2. `title`: displayed on links to your post and on top of your post's page
3. `subtitle`: displayed underneath your title on the post's page
4. `categories`: used for the categories page of your site and your posts url; if you want to use multiple categories, you can put the collection into square brackets; order matters here (going from higher to lower categories from left to right)
5. `tags`: used on the tags page of your site for the purpose of filtering; put the tags that are relevant to your post into square brackets and separate them by commas

The actual content of the post goes below the header (note that the header is delineated by `---` at the top and the bottom as can be seen above).

### Good practices

Here are some practices that work well for note taking.

#### Headings

If you created your blog by following [this tutorial](https://dev.to/teaberlin/build-an-awesome-website-for-free-59ho), you're dealing with a site that automatically creates a table of content for each of your posts based on the structure of the headings within your post. This makes navigating the content really easy for your readers. You should keep that in mind when crafting your post, because eventually this will be your go-to resource once you want to make use of the knowledge documented here.

The syntax for headings in Markdown is straight forward. `#` in front of some text turns it into a level 1 heading. `##` turns it into a level 2 heading, `###` into a level 3 heading, etc.

#### Backticks

Backticks in Markdown make it possible to format code. The following statement

~~~
```Python

print("hello world!")

```
~~~

will be formatted as


```Python

print("hello world!")

```

You can also use the three backticks without specifying the programming language.

~~~
```

print("hello world!")

```
~~~

In this case, the block between the backticks will still be treated as a code block, but it is agnostic with regard to interpreting the layout.

```

print("hello world!")

```











