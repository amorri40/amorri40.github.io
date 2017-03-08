---
layout: post
title: "Automatically Format Javascript and HTML files on Save with Grunt"
description: ""
category:
tags: []
---
{% include JB/setup %}

## Create the config
The following jobs will require a config variable is set, so it knows where all your javascript files are located.
```javascript
var config = {
    all_js_src: ['./app/**/*.js']
}
```


## Remove trailing whitespace on lines
First I wanted to automatically make sure I haven't left any trailling whitespace on any lines.
This will remove them automatically and can run on file save.
```javascript
        //
        // # Trim trailing whitespace on lines
        //  * needed as this is a warning in Sonar
        //
        trimtrailingspaces: {
            all: {
                src: config.all_js_src,
                options: {
                    filter: 'isFile',
                    encoding: 'utf8',
                    failIfTrimmed: false
                }
            }
        },
```

## FixMyJS
You will need to have created a .jshint file with your preferences in the root directory of your project.
```javascript
        //
        // FixMyJS - Automatically fixes common JS Lint erorrs
        //
        fixmyjs: {
            options: {
                config: '.jshintrc',
                indentpref: 'spaces',
                camelcase: false,
                quotemark: true,
                curly: true,
                multivar: true,
                asi: true,
                eqeqeq: true,
                ext: '.js'
            },
            all: {
                files: [{
                    expand: true,
                    cwd: './',
                    src: config.all_js_src,
                    dest: './'
                }]
            }
        },
```

## Make it beautiful
This will sort out the styling of the code to make sure all your files are consistent.
```javascript
        //
        // # Prettify Javascript files
        //
        'jsbeautifier': {
            files: config.all_js_src,
            options: {
                js: {
                    jslintHappy: false
                }
            }
        },
```

## Grunt Task
Add this grunt task to your Gruntfile.js if you want all the tasks to run as one:
```javascript
 //
    // # This task will run all the automated javascript code cleaning
    //
    grunt.registerTask('cleanjscode', [
        'trimtrailingspaces',
        'fixmyjs',
        'jsbeautifier'
    ]);
```

## Run on file Save
```
        //
        // # Watches files for changes and runs tasks based on the changed files
        //
        watch: {
            dashboardjs: {
                files: config.all_js_src,
                tasks: [
                    'cleanjscode'
                ]
            },
```

## Git commit hooks
If you want to automatically do this just before commiting you can add the following grunt task:
```javascript
        //
        // # Pre Commit Git Hooks
        //
        githooks: {
            all: {
                // Will run the jshint and test:unit tasks at every commit
                'pre-commit': 'cleanjscode'
            }
        },
```