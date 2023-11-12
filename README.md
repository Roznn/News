# News repo

This repo is currently used for testing Github as a website suitable for 
Blog posts with https://jekyllrb.com/

##  Sharing on Social media in post

- for inserting CSV data in a page
 https://jekyllrb.com/docs/datafiles/

- adding share for mastodon
  https://share-on-mastodon.social/

see ```_layouts/post.html``` 
 
## Adding favicon

in `base.html` added:

```
<link rel="shortcut icon" type="image/x-icon" href="{{ "/favicon.ico" | prepend: site.baseurl }}" > 
```

## Adding Maths/latex  


in `base.html` added:

```
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
```