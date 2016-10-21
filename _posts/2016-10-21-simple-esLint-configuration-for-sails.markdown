---
layout: post
title:  "Simple ESLint configuration for Sails JS"
date:   2016-10-21
tags: [node, eslint, sails, editor ]
---

<p class="intro"><span class="dropcap">I</span>n this post we'll look into configuring ESLint for a Sails JS application.</p>

[ESLint][eslint] is a Javascript linter that enforces best practices and helps you detect code smells like unused variables, non declared variables, tabs and spaces mixture and a lot more. Check out the ESLint rules for more examples. 

I have a [Sails JS][sails] application that needed a linter so this was a good oportunity. 

## ESLint Installation

Installing ESLint is as easy as Installing a node module (-g to install globally):

{% highlight bash %}
npm install -g eslint
{% endhighlight %}

Or adding it to the development dependencies of your current project:

{% highlight bash %}
npm install eslint --save-dev
{% endhighlight %}


## Configuring your project

Now to use ESLint in your project you need to add a <code>.eslintrc.json</code> file to the root of your project and add the following content:

{% highlight json %}
{
    "env": {
        "node": true,
        "browser": false
    },
    "parserOptions": {
        "ecmaVersion": 5,
        "sourceType": "module",
        "ecmaFeatures": {
            "jsx": false
        }
    },
    "globals": {
        "_": true,
        "sails": true,
        "async": true,
        "server": true,

        "User": true,

        "UserService": true
    },
    "extends":[
        "eslint:recommended"
    ],
    "rules":{
        "no-unused-vars": "warn",
        "no-console": "warn"
    }
}  
{% endhighlight %}

Here are several things to notice: 

* Use <code>parserOptions.ecmaVersion</code> to set your ECMAScript (Javascript) version.
* Use <code>env.node</code> and <code>env.browser</code> to identify the environment the application will run in.
* In <code>globals</code> I defined serveral global identifiers that are present in Sails JS like <code>_ (lodash), sails, async, server</code>.
* Also in <code>globals</code> I defined my project's global identifiers like <code>User, UserService</code>. Add your own models, services and controllers here.
* The <code>extends</code> array is used to add a set of recommended rules. You can extend other ESLint rules from Google, AirBnB, etc.
* In <code>rules</code> I set the project prefered rules.

## Configuring your editor

Depending on the editor you use you will find packages or extensions to enable ESLint. You can also integrate ESLint to your continous integration server.

Some examples are:

* Sublime Text [ESLint package][sublime-eslint]. 
* VSCode [ESLint extension][vscode-eslint].
* Atom [linter-eslint package][atom-eslint].

[eslint]: http://eslint.org/
[sails]: http://sailsjs.org/
[vscode-eslint]: https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint
[sublime-eslint]: https://packagecontrol.io/packages/ESLint
[atom-eslint]: https://atom.io/packages/linter-eslint
