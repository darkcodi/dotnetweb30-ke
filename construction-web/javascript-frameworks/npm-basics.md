# NPM basics:

npm is a package manager for the JavaScript programming language. It is the default package manager for the JavaScript runtime environment Node.js.

### Init project

  A `package.json` file is _always_ structured in the [JSON](http://www.json.org/) format, which allows it to be easily read as metadata and parsed by machines. 

The `npm init` command is a step-by-step tool to scaffold out your project. It will prompt you for input for a few aspects of the project in the following order:

* The project's name,
* The project's initial version,
* The project's description,
* The project's entry point \(meaning the project's main file\),
* The project's test command \(to trigger testing with something like [Standard](https://github.com/feross/standard)\)
* The project's git repository \(where the project source can be found\)
* The project's keywords \(basically, tags related to the project\)
* The project's license \(this defaults to ISC - most open-source Node.js projects are MIT\)

To create a `package.json` file with values that you supply, use the `npm init` command.

1. On the command line, navigate to the root directory of your package.

   ```bash
     cd /path/to/package
   ```

2. Run the following command:

   ```bash
     npm init
   ```

3. Answer the questions in the command line questionnaire.

 Once you run through the `npm init` steps above, a `package.json` file will be generated and placed in the current directory. If you run it in a directory that's not exclusively for your project, don't worry! Generating a `package.json` doesn't really doanything, other than create a `package.json` file. You can either move the `package.json` file to a directory that's dedicated to your project, _or_ you can create an entirely new one in such a directory.

### Install dependencies

 This command installs a package, and any packages that it depends on. If the package has a package-lock or shrinkwrap file, the installation of dependencies will be driven by that, with an `npm-shrinkwrap.json` taking precedence if both files exist. See [package-lock.json](https://docs.npmjs.com/files/package-lock.json) and [npm-shrinkwrap](https://docs.npmjs.com/cli/shrinkwrap).

 Install a standalone module into the current directory:

```bash
npm install <module>
```

In the above command, you'd replace `<module>` with the name of the module you want to install. For example, if you want to install Express \(the most used and most well known Node.js web framework\), you could run the following command:

```bash
npm install express
```

 In addition to triggering an install of a single module, you can actually trigger the installation of _all_ modules that are listed as `dependencies` and `devDependencies` in the `package.json` in the current directory. To do so, you'll simply need to run the command itself:

```bash
npm install
```

Once you run this, npm will begin the installation process of all of the current project's dependencies.

 When you're running `npm install` to install a module, you can add the optional flag `--save` to the command. This flag will add the module as a dependency of your project to the project's `package.json` as an entry in `dependencies`.

```bash
npm install <module> --save # Where <module> is the name of the module you want to install
```



### dependencies and devDependencies differences

There's a flag that is nearly an exact duplicate, in terms of functionality, of the `--save` flag when installing a module: `--save-dev`. There are a few a key differences between the two - instead of saving the module being installed and added to `package.json` as an entry in `dependencies`, it will save it as an entry in the `devDependencies`.

The semantic difference here is that `dependencies` are for use in production - whatever that would entail for your project. On the other hand, `devDependencies` are a collection of the dependencies that are used in development of your application - the modules that you use to build it, but don't need to use when it's running. This could include things like testing tools, a local server to speed up your development, and more.

```bash
npm install <module> --save-dev # Where <module> is the name of the module you want to install
```



 The final, and most common, flag for `npm install` that you should are the flags to install a module globally on your system.

{% hint style="info" %}
**Note:** One caveat with global modules is that, by default, npm will install them to a system directory, not a local one. With this as the default, you'll need to authenticate as a privileged user on your system to install global modules.

As a best practice, you should change the default installation location from a system directory to a user directory. If you'd like to learn to do this, take a peek at the seventh tip in our [npm tricks](https://nodesource.com/blog/eleven-npm-tricks-that-will-knock-your-wombat-socks-off) article!
{% endhint %}

