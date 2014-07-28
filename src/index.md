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


!SLIDE quietest shout 
# the asset you should serve<br/> is not the asset you develop


!SLIDE quietest shout
# JavaScript should be served concatenated, minified & gzipped with long-lived cache headers


!SLIDE quietest shout
# JavaScript should be developed<br/>as many small files 
## Just like your Groovy and Java code


!SLIDE quietest shout
# Your source code might not<br/>even be JavaScript 

## (i.e. CoffeeScript, ClojureScript, ES6, Dart, GrooScript, …) 


!SLIDE quietest shout
# The best place to do all<br/>of this is compile-time 

## then you're just serving static files


!SLIDE quieter shout
# Behavior<br/>With & <span class="danger">Without</span><br/>Asset-Pipeline


!SLIDE small-code danger 
## Without Asset-Pipeline
# Your layout is littered with tags

```
<link rel="stylesheet" href="/test-app/assets/main.css" />
<link rel="stylesheet" href="/test-app/assets/mobile.css" />
<link rel="stylesheet" href="/test-app/assets/app.css" />

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
<script src="/test-app/assets/app.js" type="text/javascript" ></script>
```

!SLIDE danger 
## Without Asset-Pipeline 
# Each tag is a request to the server

<img src="images/litter.png" alt="one request per tag" width="75%">

!SLIDE small-code push-content-down
## With Asset-Pipeline
# Assets transpiled, concatenated, minified, gzipped into one file per type

```
<link rel="stylesheet" href="/test-app/assets/app-08f92c4662379e3e9a56541af70c871c.css"/>

<script src="/test-app/assets/app-e1ec7cb3d4c455fac6e62f1faa6232f9.js" type="text/javascript" ></script>
```

!SLIDE push-content-down
## With Asset-Pipeline
# One server hit per file type 

<img src="images/justonehit.png" alt="one request per asset type" width="100%">


!SLIDE danger
## Without Asset-Pipeline
# Browser cache isn't properly used

<img src="images/vanilla_grails_response.png" alt="Vanilla grails response, no gzipping, bad etag" width="70%">

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
## ex: SASS, LESS, CoffeeScript, ClojureScript …

!SLIDE shout
# Developing With Asset-Pipeline 


!SLIDE 
# Files go in `grails-app/assets`

<img src="images/assetdir.png" alt="assetdir" height="80%">


!SLIDE smallish-code
# JavaScript Dependency Manifest

``` 
//= encoding UTF-8
//= require lib/angular.js
//= require_self
//= require_tree model

(function () {
  'use strict';
  console.log("loaded app.js");
  …
  });
})();
```
`assets/javascripts/app.js`


!SLIDE smallish-code
# CSS Dependency Manifest

```
/*
*= encoding UTF-8
*= require fonts
*= require bootstrap
*= require_self
*/

input.ng-invalid.ng-dirty:not(:focus) {
  border-color: #d43232;
  background-color: #f2dede;
}
…
```
`assets/stylesheets/app.css`

!SLIDE smallish-code
# Use Taglibs in Layout GSP

```
<head>
    <title><g:layoutTitle default="Some Title" /></title>
    …
    <asset:link rel="shortcut icon" href="favicon.ico" type="image/x-icon"/>
    <asset:stylesheet href="app.css"/>
    <g:layoutHead />
</head>
<body>
    <asset:image src="logo.png" width="200" height="200"/>
    …
    <g:layoutBody />
    …
    <asset:javascript src="app.js"/>
    <asset:deferredScripts/>
</body>
```
`grails-app/views/layouts/main.gsp`

!SLIDE smallish-code
# Defer JavaScript Snippets in Views

```
<div>
    <h1>foobar</h1>

    <asset:script type="text/javascript">
      console.log("on foobar page");
    </asset:script>
</div>
```
`grails-app/views/user/index.gsp`

emitted at bottom of layout at `<asset:deferredScripts/>`


!SLIDE quieter shout
# Dev Mode is Tuned for Quick Iteration

## `grails run-app`

!SLIDE smallish-code
# All Files Served With Real Names

```
// from: <asset:stylesheet href="app.css"/> 

<link rel="stylesheet" href="/myapp/assets/fonts.css" />
<link rel="stylesheet" href="/myapp/assets/bootstrap.css" />
<link rel="stylesheet" href="/myapp/assets/app.css" />
```

```
// from: <asset:javascript src="app.js"/> 

<script src="/myapp/assets/lib/angular.js" type="text/javascript" ></script>
<script src="/myapp/assets/app.js" type="text/javascript" ></script>
<script src="/myapp/assets/model/Foo.js" type="text/javascript" ></script>
<script src="/myapp/assets/model/Bar.js" type="text/javascript" ></script>
```

!SLIDE push-content-down
# In Development Files Will Not Cache

```
// HTTP 1.1
Cache-Control:no-cache, no-store, must-revalidate 

// HTTP 1.0
Pragma:no-cache 

// for proxies
Expires:Thu, 01 Jan 1970 00:00:00 GMT
```
## Response Cache Headers


!SLIDE quieter shout
# War File Serves<br/>Processed Assets

## `grails war` or `grails run-war`

!SLIDE quietest shout

# War Compilation Puts All Assets<br/>Through the Full Pipeline

## adds `assetClean` and `assetCompile` events

!SLIDE smallish-code

# War File has `assets` Folder 

```
…
assets/logo-7b9776076d5fceef4993b55c9383dedd.jpg
assets/logo.jpg
…
assets/app-2b367068131a9dd4f31c18f635eb7e6c.css
assets/app-2b367068131a9dd4f31c18f635eb7e6c.css.gz
assets/app.css
assets/app.css.gz
…
assets/app-4bf9739e18a6d5f665c42ecb7edbd339.js
assets/app-4bf9739e18a6d5f665c42ecb7edbd339.js.gz
assets/app.js
assets/app.js.gz
…
assets/manifest.properties
…
```

!SLIDE smallish-code

# Creates `manifest.properties` File With ETag Mapping For Each Asset

```
…
logo.jpg=logo-7b9776076d5fceef4993b55c9383dedd.jpg
…
app.css=app-2b367068131a9dd4f31c18f635eb7e6c.css
bootstrap.css=bootstrap-2b367068131a9dd4f31c18f635eb7e6c.css
fonts.css=fonts-81f3e38a6e878acd57e3d51912c37b04.css
…
lib/angular.js=lib/angular-de39960f9b36bbbd76e76e7ed0086922.js
app.js=app-4bf9739e18a6d5f665c42ecb7edbd339.js
…
```

!SLIDE quietest shout 

# `AssetPipelineFilter` Processes `/assets/*` Requests

!SLIDE quietest shout 
# looks for file in `/assets`<br/>if found returns (gzipped?) file<br/> with ETag from manifest


!SLIDE
# Optionally use CDN or Nginx 

```
grails.assets.url = "https://cdn.example.com/"

// or

grails.assets.url = { request ->
    if(request.isSecure()) {
        return "https://cdn.example.com/"
    } else {
        return "http://cdn.example.com/"
    }
}
```
(in `Config.groovy`)<br/>automate uploading with the cdn-asset-pipeline plugin


!SLIDE shout
# Writing Your Own Asset-Pipeline Plugin

!SLIDE smallish-code
# Implement/Override an `AssetFile`

```
package asset.pipeline

import asset.pipeline.AbstractAssetFile

class MyAssetFile extends AbstractAssetFile { // implements AssetFile

    static final String contentType = 'application/javascript'
    static extensions = ['js-myfile'] // MUST BE UNIQUE ACROSS ALL `AssetFile`s
    static final String compiledExtension = 'js'
    static processors = [MyFileProcessor]

    String directiveForLine(String line) {
        // identifies the directive in manifest lines at top of file
        // i.e. those starting with '//='
        line.find(/\/\/=(.*)/) { fullMatch, directive -> directive }
    }
}
```

!SLIDE smallish-code
# Create 1..N Processors

```
package asset.pipeline

class MyFileProcessor implements Processor {

    MyFileProcessor(AssetCompiler compiler) { 
        // compiler gives us access to the options/rules/paths 
        // that asset-pipeline is running with
        super(compiler) 
    }

    // inputText - a String holding the contents of the asset
    // assetFile - an AssetFile instance, has `file` and `baseFile` props 
    // expected to return - a String holding the processed asset text
    def process(inputText, assetFile) {
        // ex processor to turn the asset into all UPPER CASE
        return inputText.toUpperCase()
    }
}
```

!SLIDE smallish-code
# Configure Asset-Pipeline 

```
// MyAssetPipelineGrailsPlugin.groovy
import asset.pipeline.AssetHelper
import asset.pipeline.MyAssetFile

class MyAssetPipelineGrailsPlugin {
    // …

    def doWithDynamicMethods = { ctx ->
        AssetHelper.assetSpecs << MyAssetFile
    }
}
```

```
// scripts/_Events.groovy
eventAssetPrecompileStart = { assetConfig ->
  assetConfig.specs << 'asset.pipeline.MyAssetFile'
}
```

!SLIDE shout
# Asset-Pipeline AngularJS Tips


!SLIDE
# AngularJS - Minification Breaks Magic

```
// AngularJS magic injects $window using arg name
// MINIFICATION UNSAFE
myApp.controller('MyCtrl', function($window) {
    $window.alert("Hello World"); 
});

// SAFE for minification
myApp.controller('MyCtrl', ['$window', function($window) {
    $window.alert("Hello World");
}]);
```

Either turn variable mangling off in `Config.groovy` or <br/> use Craig Burke's angular-annotate-asset-pipeline plugin

!SLIDE smallish-code push-content-down
# angular-template-asset-pipeline 

```
// original: /grails-app/assets/templates/my-app/app-section/index.tpl.htm
// <h1>Hello World!</h1>

angular.module('myApp.appSection')
       .run(['$templateCache', function($templateCache) {
    $templateCache.put('index.htm', '<h1>Hello World!</h1>');
}]);
```
## Compile HTML templates Into `$templateCache`


!SLIDE quieter shout
# Advantages Over the Resources Plugin


!SLIDE quieter shout
# Allows the use <br/>of a CDN


!SLIDE quieter shout
# No Waiting to Recompile in Development


!SLIDE quieter shout
# Precompilation Allows Faster War Startup


!SLIDE quieter shout
# Dependencies Are Inside Assets


!SLIDE quieter shout
# Actively Developed


!SLIDE shout
# Migrating from Resources Plugin


!SLIDE 

# Resources

## layout: `<r:require modules="app"/>` 

<br/>
# Asset-Pipeline

## layout: `<asset:stylesheet href="app.css"/>` 
## bottom of layout &lt;body&gt;: `<asset:javascript src="app.js"/>` 

!SLIDE 

# Resources

## `<r:external uri="/img/favicon.ico"/>`
<br/>
# Asset-Pipeline

## `<asset:link rel="shortcut icon" href="favicon.ico" type="image/x-icon"/>`

!SLIDE 

# Resources

## `<g:img dir="img" file="logo.jpg" alt="The Logo" />`

<br/>
# Asset-Pipeline

## `<asset:image src="logo.png" alt="The Logo"/>`

!SLIDE 

# Resources

## gsp: `<r:script disposition="defer">alert('foo');</r:script>`
## layout: `<r:layoutResources/>` 

<br/>
# Asset-Pipeline

## gsp: `<asset:script>alert('foo');</asset:script>`
## layout: `<asset:deferredScripts/>` 

!SLIDE 

# Resources

## in gsp: `href="${resource(dir: 'css', file: 'errors.css')}"`

<br/>
# Asset-Pipeline

## in gsp: `href="${asset.assetPath(src: 'errors.css')}"`


!SLIDE shout
# Asset-Pipeline Alternatives


!SLIDE quieter shout
# gradle 
## not part of grails build without more work, <br/> doesn't solve caching/etags


!SLIDE quieter shout
# grunt/gulp 
## requires buy-in/support of node.js <br/>ecosystem, doesn't solve caching/etags


!SLIDE quieter shout
# resources plugin 
## deprecated, more painful to work with


!SLIDE shout
# Questions? 
