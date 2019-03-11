---
title: Where do I start? Part2: CSS Pre-Processors
published: true
description: A short blog with some list of links and guides for folks starting out.
tags: beginners, webdev, sass, css
---
# Where do I start? Part2: CSS Pre-Processors ~~and JavaScript~~
## Last time...
Last time I posted in **[part-0](https://dev.to/kevindsteeleii/where-do-i-start-part-0-bash-terminal-git-and-github-version-control-3287)** some of the things you may want to start doing before working on anything in **[part-1](https://dev.to/kevindsteeleii/where-do-i-start-part1-ides-html-css--css-frameworkslibraries-3acb)**. We'll start off with the assumption that you have a decent grasp of both HTML && CSS, you can use a text editor, and know enough git and command line commands to do most of what you need without using a UI.

## I know HTML, CSS, and all that, now what?
So if you're feeling this way, you've probably done some if not all of the following:
1. Made a static website
2. Learned Mobile first or Responsive styling
3. Worked on **[Free Code Camp Responsive Web Design Projects](https://learn.freecodecamp.org/responsive-web-design/responsive-web-design-projects/)** or projects like them. 

If not, you can start with these **[HTML](https://learn.freecodecamp.org/responsive-web-design/basic-html-and-html5)** or **[CSS](https://learn.freecodecamp.org/responsive-web-design/basic-css)** courses at Free Code Camp or use whatever resource/s that best suit your learning style and needs/goals. If you want to code as a hobby, that's fine too. I'll save the **JavaScript** post for later because the length of this one has become a bit much.

## CSS Pre-Processors ~~and JavaScript~~
Modern CSS makes it much easier to style pages than compared with the bye-gone days of MySpace pages and Friendster. But even if you adopt amazing CSS architectures like **[SMACCSS](https://smacss.com/)** or stick to your basic **[BEM](http://getbem.com/)**, large or complex projects can make it harder to generate lean, effective CSS. Enter CSS Pre-Processors, they generate CSS thus the name and they have really neat functionality. Such as:
  - less stuffy syntax
  - nested selectors to simplify and cut down on classes and modifier use 
  - has data types you can use for better interaction
  - functions w/ arguments
  - control flow 
  - and more!!

### I'll give an example using SCSS
You want to perfectly center a tag in relation to its height but it's also nested in another tag but the parent's positioning is absolute or relative to its own parent. What would we do?
  ```scss
  /* In CSS */
  div.parent {
    position: absolute;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
  }

  /* Had to write a specific selector */
  div.parent > div.child {
    --child-height--: 35vh;
      position: inherit;
      margin: 0 auto;
      /* Seems like a lot to write just for this */
      margin-top: calc(50vh - calc(var(--child-height--)/2));
      width: 35vw;
      height: var(--child-height--);
  }

  /* In SASS */
  $child-height: 20vh; // reuseable in multiple places

  div.parent {
    position: absolute;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;

    div.child {
      position: inherit;
      margin: 0 auto;
      margin-top: 50vh - $child-height/2; /* Cleaner */
      width: 35vw;
      height: $child-height;
    }
  }
  ```
  Now imaging adding more tags and styling where that came from. You can imagine the mess that your CSS files could become. Before the advent of CSS Pre-Processors you had to write more selectors, use more classes, and it lacked the extensive functionality afforded by CSS Pre-Processors like SASS.

### Resources
- Documentation
	- [SASS](http://sass-lang.com/documentation/file.SASS_REFERENCE.html)
	- [LESS](http://lesscss.org/#)
	- [STYLUS lang](http://lesscss.org/#)
	- [post CSS](https://postcss.org/)
- Videos
    - [Sass Crash Course by DesignCourse](https://www.youtube.com/watch?v=roywYSEPSvc&t=5s)
    - [LESS CSS Pre-Processor Tutorial by Traversy Media](https://www.youtube.com/watch?v=YD91G8DdUsw)

### Next time
Next time we'll finally look at JavaScript. A brief overview of the basic syntax and control-flow, recommended reading, and other resources. As always, I'm new so I acknowledge that I may make mistakes and am open to critique, discourse, or suggestions. Thank you!!