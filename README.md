# clauswilke.github.io

This site uses the bootstrap framework. The following explains how I incorporated it into the site.

## Bootstrap sass

As described here: http://veithen.github.io/2015/03/26/jekyll-bootstrap.html

1. Download latest version from here: https://github.com/twbs/bootstrap-sass/tags. It is currently 3.3.5.
2. Copy the following files and directories from the archive to `_sass`:  
`assets/stylesheets/_bootstrap.scss`  
`assets/stylesheets/bootstrap`
3. Create a basic stylesheet (e.g. `assets/css/site.scss`) as follows:  
```
---
---
    
@import "bootstrap";
```
All variable definitions etc. need to be made before the final `@import "boostrap";` line.


## Bootstrap javascript

Documentation: http://getbootstrap.com/javascript/

1. Move `bootstrap.min.js` from the bootstrap archive to `assets/javascript/`.
