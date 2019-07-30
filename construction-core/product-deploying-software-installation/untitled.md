# Manage packages by using NuGet, NPM and Bower

### **NuGet**

{% hint style="success" %}
**NuGet** is a dotnet package management system for Visual Studio.
{% endhint %}

It makes it easy to add, update and remove external libraries in our application. Using NuGet, we can create our own packages easily and make it available for others.

#### Install package with Nuget

To install a new package, use the following command:

`Install-Package (PackageName)`

#### Update package with Nuget

To update existing package use this:

`Update-Package (PackageName)`

If you want to update a certain package, then use -version switch like below:

`Update-Package Elmah -version 1.1`

### **NPM**

{% hint style="success" %}
The **Node Package Manager \(npm\)** is a command-line tool used by developers to share and control modules \(or packages\) of JavaScript code written for use with Node.js.
{% endhint %}

When starting a new project, npm generates a `package.json` file. This file lists the package dependencies for your project. Since npm packages are regularly updated, the `package.jsonfile` allows you to set specific version numbers for each dependency. This ensures that updates to a package don't break your project.

Npm can save packages in two ways:

1. **Globally** in a root `nodemodules` folder, accessible by all projects.
2. **Locally** within a project's own `node_modules` folder, accessible only to that project.

### Bower

{% hint style="success" %}
**Bower** offers a generic, unopinionated solution to the problem of **front-end package management**, while exposing the package dependency model via an API that can be consumed by a more opinionated build stack
{% endhint %}

It can manage components that contain HTML, CSS, JavaScript, fonts or even image files.

Bower doesn’t concatenate or minify code or do anything else - it just installs the right versions of the packages you need and their dependencies.

Bower requires node, npm and git. It keeps track of these packages in a manifest file, `bower.json`.

#### **Install Bower with npm**

Bower is a command line utility. Install it with npm:

`$ npm install -g bower`

#### Install packages with bower

Bower installs packages to `bower_components`:

`$ bower install (package)`

#### Save package with bower

Create a `bower.json` file for your package with `bower init` command. Then save new dependencies with `bower install PACKAGE --save`.

```text
<script src="bower_components/jquery/dist/jquery.min.js"></script>
```

