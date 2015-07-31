# clauswilke.github.io


## Bootstrap sass

As described here: http://veithen.github.io/2015/03/26/jekyll-bootstrap.html

1. Download latest version from here: https://github.com/twbs/bootstrap-sass/tags. It is currently 3.3.5.
2. Copy the following files and directories from the archive to `_sass`:  
`assets/stylesheets/_bootstrap.scss`  
`assets/stylesheets/bootstrap`
3. Create a basic stylesheet (e.g. `css/site.scss`) as follows:  
```
---
---
    
@import "bootstrap";
```


## Bootstrap javascript

Documentation: http://getbootstrap.com/javascript/

1. Move `bootstrap.min.js` from the bootstrap archive to `assets/javascript/`.
