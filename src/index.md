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
# Behavior<br/>With & <span class="danger">Without</span><br/>Asset-Pipeline

## (or the resources plugin)


!SLIDE small-code danger 
## Without Asset-Pipeline
# Your layout is littered with tags

```
<link rel="stylesheet" href="/test-app/assets/main.css" />
<link rel="stylesheet" href="/test-app/assets/mobile.css" />
<link rel="stylesheet" href="/test-app/assets/application.css" />

<script src="/test-app/assets/vendor/angular/angular-route.js" type="text/javascript" ></script>
<script src="/test-app/assets/vendor/jquery/jquery.js" type="text/javascript" ></script>
<script src="/test-app/assets/vendor/mongolab/mongolab-resource.js" type="text/javascript" ></script>
<script src="/test-app/assets/app/admin/admin.js" type="text/javascript" ></script>
<script src="/test-app/assets/app/admin/projects/admin-projects.js" type="text/javascript" ></script>
<script src="/test-app/assets/app/admin/users/admin-users-edit.js" type="text/javascript" ></script>
<script src="/test-app/assets/app/admin/users/admin-users-list.js" type="text/javascript" ></script>
<script src="/test-app/assets/app/admin/users/admin-users.js" type="text/javascript" ></script>
<script src="/test-app/assets/app/admin/users/uniqueEmail.js" type="text/javascript" ></script>
<script src="/test-app/assets/app/admin/users/validateEquals.js" type="text/javascript" ></script>
<script src="/test-app/assets/app/app.js" type="text/javascript" ></script>
<script src="/test-app/assets/app/dashboard/dashboard.js" type="text/javascript" ></script>
<script src="/test-app/assets/app/projects/productbacklog/productbacklog.js" type="text/javascript" ></script>
<script src="/test-app/assets/app/projects/projects.js" type="text/javascript" ></script>
<script src="/test-app/assets/app/projects/sprints/sprints.js" type="text/javascript" ></script>
<script src="/test-app/assets/app/projects/sprints/tasks/tasks.js" type="text/javascript" ></script>
<script src="/test-app/assets/app/projectsinfo/projectsinfo.js" type="text/javascript" ></script>
<script src="/test-app/assets/application.js" type="text/javascript" ></script>
```

!SLIDE danger 
## Without Asset-Pipeline 
# Each tag is a request to the server

<img src="images/litter.png" alt="one request per tag" width="78%">

!SLIDE small-code push-content-down
## With Asset-Pipeline
# Assets transpiled, concatenated, minified, gzipped into one file per type

```
<link rel="stylesheet" href="/test-app/assets/application-08f92c4662379e3e9a56541af70c871c.css"/>

<script src="/test-app/assets/application-e1ec7cb3d4c455fac6e62f1faa6232f9.js" type="text/javascript" ></script>
```

!SLIDE push-content-down
## With Asset-Pipeline
# One server hit per file type 

<img src="images/justonehit.png" alt="one request per asset type" width="100%">


!SLIDE danger
## Without Asset-Pipeline
# Browser cache isn't properly used

<img src="images/vanilla_grails_response.png" alt="Vanilla grails response, no gzipping, bad etag" width="73%">

!SLIDE  
## With Asset-Pipeline
# Initial Request - Good Cache Headers

<img src="images/AP_grails_response.png" alt="etags, expires, gzipping, etc" width="100%">


!SLIDE  
## With Asset-Pipeline
# Next Request - Cache Hit

<img src="images/AP_grails_cached_response.png" alt="etags, expires, gzipping, etc" width="90%">


!SLIDE danger push-content-down
## Without Asset-Pipeline
# Limited to browser-supported languages 
## i.e. CSS and JavaScript


!SLIDE push-content-down
## With Asset-Pipeline
# Can use anything that transpiles to browser-supported languages
## ex: SASS, LESS, CoffeeScript, ClojureScript, Dart, TypeScript…

!SLIDE shout
# Developing With Asset-Pipeline 


!SLIDE 
# Files go in `grails-app/assets`

<img src="images/assetdir.png" alt="assetdir" height="80%">


!SLIDE 
# TODO START HERE

!SLIDE 
# file types with manifest comments in them

!SLIDE
# taglibs in gsps

```
  asset:image
```

!SLIDE
# dev mode goes through asset controller

!SLIDE
# assets served as individual files

```
show generated html
```

set to never cache


!SLIDE shout
# How Asset-Pipeline Works In Production


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

- angular mangling off for minifcation, or use angular plugin
- cdn support
- other plugins
- write your own asset pipeline plugin


!SLIDE quieter shout
# Advantages over Resources Plugin


!SLIDE quieter shout
# no waiting to recompile in development

!SLIDE quieter shout
# precompilation means easier troubleshooting & faster war startup

!SLIDE quieter shout
# dependencies are with assets

!SLIDE shout
# Migrating from Resources Plugin

!SLIDE quieter shout
# TODO: insert resources rosetta stone


!SLIDE shout
# Asset-Pipeline Alternatives


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
