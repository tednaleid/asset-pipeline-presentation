# Grails Asset-Pipeline Plugin


by <a href="https://twitter.com/tednaleid">@tednaleid</a>

!SLIDE quieter shout

# Using Grails<br/>Asset-Pipeline 

## by <a href="https://twitter.com/tednaleid">@tednaleid</a>

!SLIDE shout

# What is an &#8220;asset&#8221;?

!SLIDE quietest shout 
# assets are &#8220;static&#8221; files<br/><br/>CSS, JavaScript, HTML &amp; Images

!SLIDE shout

# Why do assets need a &#8220;pipeline&#8221;?


!SLIDE quieter shout 
# the asset you should serve is not the asset you develop

!SLIDE quietest shout

# JavaScript should be served concatenated, minified & gzipped with long-lived cache headers

!SLIDE quietest shout

# JavaScript should be developed<br/>as many small files 
## Just like your Groovy and Java code

!SLIDE quietest shout

# Your source code might not even be JavaScript 

## (i.e. CoffeeScript, ClojureScript, ES6, Dart, TypeScript, …) 

!SLIDE quieter shout

# The best place to do all of this is compile-time 

## then you're just serving static files


!SLIDE shout

# Status Quo

!SLIDE shout

# How You Develop With It

!SLIDE quietest shout

- put everything in assets
- file types with manifest comments in them
- taglibs in gsps
  - asset:image
- dev mode asset controller?

!SLIDE shout

# How it Works In Production

!SLIDE quietest shout

- war compilation
- war creates manifest.properties file
- static assets in `assets` folder in the war file

!SLIDE quietest shout

- `AssetPipelineFilter` added to `web.xml`
- request for asset meets filter
- looks for file
- not found 404
- if found looks for etag in manifest
- returns with etag and `Vary: Accept-Encoding`

!SLIDE quietest shout

# Compilation Sausage Factory

- AssetFile (1 per file)
- processor
- post processor?
- look at plugin.groovy file for other details


!SLIDE quieter shout
#  tips
- angular mangling off for minifcation
- cdn support
- other plugins
- write your own asset pipeline plugin
- dynamic links in JS, compiling into template cache

!SLIDE quieter shout
# changes from resources







!SLIDE 
<br/>
# commit

A slide with code both `inline` and in a block:

```
here is some code
    indented
```


!SLIDE

# Look! An Image!

<img src="images/linen.png" alt="">


!SLIDE shout
# Danger!

<span class="danger">dangerous</span>


!SLIDE shout
# Questions? 


