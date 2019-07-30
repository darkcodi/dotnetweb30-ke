# SDO Best Practices Catalog - Automatic Code Inspection

### Benefits

Automatic code inspection that is run on regular intervals:

* forces code conventions across the team and reduces code duplication in real time during development
* educates the development team and prevents the code from anti-patterns and bad practices
* introduces an approach for source code technical debt tracking
* visualize the source code quality indicators for a team and management
* accelerates the code review and offloads a code reviewer

### Indicators of successful process

* The automatic code inspection procedure is defined and communicated to team
* Code analysis tool is automatically run on a regular intervals or certain events \(commit, build, at specific time\) during all development process
* Code conventions are checked by automatic code inspection
* Code analysis is set up on both developer's and CI machines
* Custom code analysis rules are defined to meet project specifics
*  Code analysis is run against DB scripts and tests source code
*  Code duplication detection tools are used
* Static code analysis is made against following issues:
* * * Logical errors
    * API misuse
    * Typographical errors \(in strings, comments\)
    * Security
    * Threads and synchronization
    * Performance and optimization
* Flow analysis is conducted against following issues:
* * * Exceptions
    * Optimization
    * Resource leaks
    * API misuse
    * Security
*  Goals based on code metrics are explicitly linked to project goals and set when necessary
* Metrics linked to code quality goals are collected and reviewed on a regular intervals
* Metrics gathering is automated
* The code inspection issues are tracked and fixed regularly 

### Tools

* SonarQube
* Resharper       
* TFS/Visual Studio 
* FXCop   
* StyleCop

