---
title: no office suites
tags:
  - office
  - markdown
  - pandoc
  - git
---

Why do people still use office suites?

I don't want to.

It annoys me.

Now it has version control, but its crappy, too.

## use git

Anything that does not support git is not worth using.

## high quality output

Not with office suites. Formatting always looks bad and unprofessional. The way to go is LaTeX. But writing LaTeX sucks because its very verbose. Take blogging: I don't write HTML and I most certainly want to use a crappy *rich* text editor on the web or a weird CMS that doesn't do what I want as well. I write in Markdown. With **pandoc** I can write my documents in Markdown, too. And I can use git for version control. And I can use platforms like GitHub or GitLab to collaboratively work with people on documents.

## just for tech people?

At the moment, this only works for nerds. Can my mom install and use pandoc? I don't think so.

What do we need to make this available to a broader audience (besides IT education)?

- a relatively dumb text editor
- HTML preview or possibly side-by-side view
- git integration
  - maybe a platform dedicated to documents, not primarily for software
    - with a CI / CD to build / publish the docs
  - account / authentication integration
  - simple history
  - an integrated merge tool
- LaTeX / pandoc integration to create the PDF

The LaTeX and pandoc integration may probably not be practical on mobile devices, just because of the sheer amount of disk space required for TeX Live and Haskell.

## How can we sell this to non-technical people?

Let me know!
