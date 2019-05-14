<a name="bestPractices"></a>
# XY Bootstrap and Bootstrap Framework Standards

## Bootstrap
Bootstrap is a free CSS framework that is comprised of multiple CSS components, Sass variables, and some Javascript. It is maintained frequently and offers a wide range of components, while also allowing for CSS overriding through the use of Sass variables. The Bootstrap website can be viewed [here.](https://getbootstrap.com/) The latest version is Bootstrap 4.

### SCSS & Sass Variables
Sass variables allow XY to override default colors, shaping, structure, and manipulation of components, without the need for excessive code. For example, the in-line styles for overriding Bootstrap's light background class, or `bg-light` class might look something like:
```html
<div class="bg-light" style="background-color:red">
```
or worse,
```html
<div class="bg-light" style="background-color:red!important">
```
Instead, Sass variables allow you to override the Bootstrap color for "light" at the top level like so:
```scss
$red: #4256c4;
$theme-colors: (light: $red);
```
As a result, red wil now be defined by `#4256c4;`, and that defined variable of `$red` will now take the place for any `light` variations in Bootstrap. This means it will affect light backgrounds, buttons, modals, text, and more.

The documentation for SCSS and Sass variables can be found [here.](https://sass-lang.com/documentation/syntax)

### Compiling + CodeKit
#### Compiling HTML - CodeKit
XY compiles all HTML with "CodeKit". The documentation can be found [here.](https://codekitapp.com/)
#### Code Kit Variables
Learn more about Code Kit Variables here: https://codekitapp.com/help/kit/

#### SEO + Code Kit
The meta tags for each page use Code Kit Variables so each page can have dynamic content.

The two variables are `$title` and `$desc`, for `<title>` and `<meta name="description">`, respectively.

You may receive the following error that looks something like this if you forget to assign a value to these variables on a website's page:
```
Line 16 of head.kit: The variable $title is undefined.
```

If your website will not need a title and description on every page, use Code Kit's "Optional" notation for variables, which is noted by a `?` at the end of the variable. Here's an example:

```
<dl>
  <dd class='<!-- $myVar? -->'> Page 1 </dd>
  <dd class='<!-- $otherVar? -->'> Page 2 </dd>
</dl>
```

Note: This was unsuccessful with the `description` variable, likely because the syntax was errored with the "" around the variable.

However, please know that for SEO purposes, it is extremely valuable to have a title and description on each page in your website, so Google can properly crawl and display your site. It will also help with social posts and sharing links to your website, because the meta data can properly populate a sneak view of your webpage.

### Editor
For Bootstrap-built projects, the default editor should be Visual Studio Code (VS Code). Download the application [here](https://code.visualstudio.com/).

### Lint
Any project using Bootstrap should utilize the following VS Code Lint extensions:
- HTMLHint _(by Mike Kaufman)_
- ESLint _(by Dirk Baeumer)_
- TSLint (deprecated) _(by egamma)_

### Compiling - Other
#### Compiling Javascript
XY compiles all Javascript with "BabelJS". The documentation can be found [here.](https://babeljs.io/)

### CI / CD

[Travis CI](https://travis-ci.org/) provides an automated build service for projects, with the ability to run unit and UI tests as part of the build. In order for this to be most effective, the `master` and `develop` branches for a GitHub repository should be locked, with pull requests automatically kicking off a Travis build which would utilize Fastlane for running tests, computing test coverage, and deploying the build to Test Flight if so desired. 

> Setup instructions to follow soon

Note: this copy was taken from Darren's MACOS standards.

### Allowed Technologies
- Bootstrap 4
- 
### Other Best Practices

#### Other VS Code Extensions
- Beautify _(by HookyQR)_

#### Using Design Systems + Creating Constraints

Even if you are not a web designer, you should build a design system and create constraints that will allow you to produce a bare-bones product with decent design. Bootstrap will already set you up for success, thanks to limited colors like `primary`, `danger`, `light` and so on. While you're already set up with multiple hues (red, green, blue, etc), you can extend the color saturation range to add more flair to a project.

An easy way to experiment with colors, hues, and saturation is with a visual tool like [Material.io.](https://material.io/tools/color/#!/?view.left=0&view.right=0&primary.color=6002ee) You can see an example of the XY Company Website [here.](https://material.io/tools/color/#!/?view.left=0&view.right=0&primary.color=0023F5#0023F5%2F%3Fview.left=0&view.right=0)

<a name="sassUI"></a>
### XY Standard Sass Variables
Although Bootstrap offers many color and sizing options with their default Sass variables, others can be created for a more effective design flow of the project.

Remember you will still need to put these new variables into the `$theme-colors` list:

```$theme-colors: (primary: $blue, secondary: $teal);```
would become
```$theme-colors: (primary: $blue, secondary: $teal, primary-muted: $primary-muted);```

| XY Sass Variables | Purpose                                                                      |
| -------------------| --------------------------------------------------------------------------- |
| `$primary-muted`   | Muted primary color for backgrounds and other components                    |
| `$secondary-muted` |   Muted secondary color for backgrounds and other components                |
| `$light-offset`    |  An offset for light websites, for visual differentiation without overpower |
| `$dark-offset`     |  An offset for dark websites, for visual differentiation without overpower  |
| `$primary-bright` or  `$primary-dark`|  A highly saturated or darkened primary color for text on colored backgrounds or as an accent color. Read #2 in [this article](https://medium.com/refactoring-ui/7-practical-tips-for-cheating-at-design-40c736799886) to learn more.       |
| `secondary-bright` or `$primary-dark` |  A highly saturated or darkened secondary color for text on colored backgrounds or as an accent color. Read #2 in [this article](https://medium.com/refactoring-ui/7-practical-tips-for-cheating-at-design-40c736799886) to learn more. |

##### Best Practice Example 1: Text Pop
This is an example of when `$primary-bright` can be used to create text that pops off a `bg-primary` component.

![example1-image](https://cdn-images-1.medium.com/max/1600/1*ajjrhpp-l3GDG7ne7Am8fw.png)
(Example from Refactoring UI - https://refactoringui.com/)

##### Best Practice Example 2: Visual Differentiation
This is an example of when `light-offset` can be used to create visual differentiation on a component.

![example2-image](https://cdn-images-1.medium.com/max/2400/1*fNm6hXxnBvIcHGp9DQRdRQ.png)
(Example from Refactoring UI - https://refactoringui.com/)

##### Best Practice Example 3: Color Variation
This is an example of how different variations of the default Bootstrap `primary` can be combined to create a project with [multiple elevations](https://material.io/design/environment/elevation.html#depicting-elevation) and optimal readability.

![example3-image](https://storage.googleapis.com/spec-host-backup/mio-design%2Fassets%2F1H9ZMgMwTh3usXcum_NtXvF-BC5XDwDoo%2Fcolor-applyingcolorui-surfaces-surfaceelevations-crane.png)
(Example from Material Design - https://material.io/)