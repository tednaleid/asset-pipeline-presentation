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


!SLIDE quieter shout
# Behavior<br/>With & Without<br/>Asset-Pipeline

## (or the resources plugin)


!SLIDE  
## Without Asset-Pipeline
# Your layout is littered with CSS & JS tags

```
TODO: insert angular/lodash/moment/etc example
//maybe from angular js bootstrap?
<script src='foo.js'></script>
```

!SLIDE  
## With Asset-Pipeline
# Assets concatenated, minified, gzipped into a single file per type

```
TODO: insert angular/lodash/moment/etc example
//maybe from angular js bootstrap?
<script src='foo.js'></script>
```




!SLIDE  
## Without Asset-Pipeline
# Dependencies are difficult to manage and maintain

```
TODO: insert angular/lodash/moment/etc example
// explain how all files are in one place, deleting a file doesn't delete dependencies
```

!SLIDE  
## With Asset-Pipeline
# Dependencies are specified within each file, allows inclusion of directories and trees

```
TODO: show how dependencies are in top of file
```

!SLIDE  
## Without Asset-Pipeline
# Browser cache isn't properly used

<img src="images/vanilla_grails_response.png" alt="Vanilla grails response, no caching, reloads every time">

!SLIDE  
## With Asset-Pipeline
# Browser Cache Leveraged

<img src="images/AP_grails_response.png" alt="etags, expires, gzipping, etc">


!SLIDE  
## Without Asset-Pipeline
# Limited to browser-supported languages 
## i.e. CSS and JavaScript


!SLIDE  
## With Asset-Pipeline
# Can use anything that compiles to browser-supported languages
## ex: CoffeeScript, ClojureScript, Dart, TypeScript, SASS, LESS, etc


!SLIDE shout
# Current Plugins???
- coffeescript
- sass
- angularjs
- others


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
- war creates manifest.properties file with etag mapping for each asset
- static assets in `assets` folder in the war file


!SLIDE quietest shout

- `AssetPipelineFilter` added to `web.xml`
- request for asset meets filter
- looks for file
- not found 404
- if found looks for etag in manifest
- returns gzipped file with etag and `Vary: Accept-Encoding`


- cdn support?


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
# Advantages over Resources Plugin


!SLIDE quieter shout
# no waiting to recompile in development

!SLIDE quieter shout
# precompilation means easier troubleshooting & faster war startup

!SLIDE quieter shout
# dependencies are with assets

!SLIDE quieter shout
# Migrating from Resources Plugin


!SLIDE quieter shout
# insert resources rosetta stone







!SLIDE shout
# Asset-Pipeline Alternatives

!SLIDE quieter shout
# Alternatives in Grails

!SLIDE quieter shout
# gradle 
## weak JS support, not part of grails build without more work, doesn't solve caching/etags

!SLIDE quieter shout
# grunt/gulp 
## requires buy-in/support of node.js ecosystem, doesn't solve caching/etags

!SLIDE quieter shout
# resources plugin 
## deprecated, more painful to work with

!SLIDE shout
# Questions? 
