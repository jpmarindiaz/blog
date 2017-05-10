---
title: Gitbook cheatsheet
lang: en
date: 2016-12-02 18:50:16
categories:
    - Dev
tags:
---


# Create a book

GitBook can setup a boilerplate book:

```
gitbook init
```

If you wish to create the book into a new directory, you can do so by running gitbook init ./directory

Preview and serve your book using: `gitbook serve`
Or build the static website using: `gitbook build`

Generate a PDF file `gitbook pdf ./ ./mybook.pdf`
Generate an ePub file `gitbook epub ./ ./mybook.epub`
Generate a Mobi file `gitbook mobi ./ ./mybook.mobi`


# Plugins

```
    "plugins": ["hide-published-with","addcssjs", "sharing", "footnote-string-to-number", "richquotes", "emphasize", "image-captions", "atoc", "katex", "autosize-iframe", "collapsible-menu", "printlinks"],
```

## Plugin 
image-caption
```
            "attributes": { "width": "300" },
```



# Markdown


## Intro

```
Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
consequat. [1]

| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |

Duis aute irure dolor in reprehenderit in voluptate velit esse
cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non
proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

This is some text[^1].

[^1]: Some *crazy* footnote definition.


## Rich quotes

> **Info** Info


> **Note** Note


> **Tag** Tag


> **Comment** Comment

> **Hint** Hint

> **Success** Success

> **Warning** Warning

> **Caution** Caution

> **Danger** Danger

> **Quote** Quote

## Text highlight

This text is {% em %}highlighted !{% endem %}

This text is {% em %}highlighted with **markdown**!{% endem %}

This text is {% em type="green" %}highlighted in green!{% endem %}

This text is {% em type="red" %}highlighted in red!{% endem %}

This text is {% em color="#ff0000" %}highlighted with a custom color!{% endem %}

![imagesss](assets/images/business-sprint.png)

![Alt text][id]

[id]: assets/images/business-backlog.png  "Optional title attribute"
```


