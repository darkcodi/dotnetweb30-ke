# Integrating with Issue Tracking Systems

* **TFS** Team Foundation Server is a Microsoft product that provides source code management \(either with Team Foundation Version Control or Git\), reporting, requirements management, project management \(for both agile software development and waterfall teams\), automated builds, lab management, testing and release management capabilities. It covers the entire application lifecycle, and enables DevOps capabilities.TFS can be used as a back-end to numerous integrated development environments \(IDEs\) but is tailored for Microsoft Visual Studio and Eclipse on all platforms.
* **TortoiseGit** can help the user in two ways:

  1. When the user enters a log message, a well defined line including the issue number associated with the commit can be added automatically. This reduces the risk that the user enters the issue number in a way the bug tracking tools can't parse correctly.

     Or TortoiseGit can highlight the part of the entered log message which is recognized by the issue tracker. That way the user knows that the log message can be parsed correctly.

  2. When the user browses the log messages, TortoiseGit creates a link out of each bug ID in the log message which fires up the browser to the issue mentioned.

  TortoiseGit can be configured to associate issue tracker plugin with your project.

* **Jira** is a proprietary issue tracking product developed by Atlassian that allows bug tracking and agile project management. Such apps as Git Integration for Jira are for your existing Jira Server/Cloud instance that combines the data in your Git repository with the projects and issues in Jira.
* **GitLab** The GitLab issue tracker is an advanced tool for collaboratively developing ideas, solving problems, and planning work.
* **GItHub** You can collect user feedback, report software bugs, and organize tasks you'd like to accomplish with issues in a repository. Issues can act as more than just a place to report software bugs. Issues can also be assigned to other users,tagged with labels for quicker searching, and grouped together with milestones.

