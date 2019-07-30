# Automated build concept

### **Definition**

In the context of software development, build refers to the process that converts files and other assets under the developers’ responsibility into a software product in its final or consumable form. The build may include:

* compiling source files 
* packaging compiled files into compressed formats \(such as jar, zip\) 
* producing installers creating or updating of database schema or data

### **Expected Benefits**

Build automation is a prerequisite to effective use of continuous integration. However, it brings benefits of its own:

* eliminating a source of variation, and thus of defects; a manual build process containing a large number of necessary steps offers as many opportunities to make mistakes 
* requiring thorough documentation of assumptions about the target environment, and of dependencies on third party products

### Common Pitfalls

* the practice of build automation should not be confused with continuous integration: the latter consists of “executing” the build process as frequently as possible \(ideally whenever a code change is checked into the source code control repository\) and “verifying” the correctness of the resulting product, in particular by unit tests 
* in particular, continuous integration tools \(CruiseControl, Hudson, etc.\) are a category distinct from build automation tools \(make, Ant, Maven, rake, etc.\) 
* being able to trigger some build operations from within a development environment \(IDE\) is usually not sufficient: as it is often the case that some build operations are not supported within the IDE, it must be possible to perform a build outside of the IDE 
* the duration of a build process should be under ten minutes, including the execution of automated tests; beyond this order of magnitude it will generally be difficult for the team to achieve continuous integration

### Signs of Use

The best way to ascertain whether a team practices build automation is a surprise test: ask the team to provide an installable version of the product. Measure how much time is necessary to obtain a release, then attempt to install or deploy to an off the shelf PC or environment – one which has not been previously set up by the development team. Any “surprise” during this process will suggest ways to improve the automated build process.

