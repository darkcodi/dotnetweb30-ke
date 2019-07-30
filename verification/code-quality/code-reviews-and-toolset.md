# Code Reviews and Toolset

###  Code Review Process

![](../../.gitbook/assets/image%20%2836%29.png)

### Review Process Metrics

**Inspection Rate**

This metric can be used to get a rough idea of the required duration to perform a code review. The inspection rate is the rate of coverage a code reviewer can cover per unit of time. From experience, a rate of 250 lines per hour would be a baseline. This rate should not be used as part of a measure of review quality, but simply to determine duration of the task.

**Defect Detection Rate**

This metric measures the defects found per unit of time. Again, can be used to measure performance of the code review team, but not to be used as a quality measure. Defect detection rate would normally increase as the inspection rate \(above\) decreases.

**Code Coverage**

Measured as a % of LoC of function points, the code coverage is the proportion of the code reviewed. In the case of manual review we would aim for close to 100%, unlike automated testing wherein 80-90% is considered good. In order to ensure that the code coverage standards are met, some organizations might implement a safety check during the build process, so the build will fail if there are any piece of code that has not been tested or if it the coverage is under the desired percentage. The higher the percentage of code coverage, the better to ensure quality and prevent logic errors.

**Defect Correction Rate**

The amount of time used to correct detected defects. This metric can be used to optimise a project plan within the SDLC. Average values can be measured over time, producing a measure of effort which must be taken into account in the planning phase.

**Reinspection Defect Rate**

The rate at which upon re-inspection of the code more defects exist, some defects still exist, or other defects manifest through an attempt to address previously discovered defects.

**Size of a review change set**

Strictly enforce limits on the size of a review change set. Effectiveness in reviews begins decreasing after the first 15 minutes spent reviewing and drops drastically after 60 minutes. Respecting this practice will also help when bisecting code history during bug hunting.

**Roles for a code review process**

* **Referee** - he/she is responsible for making sure that the code review meeting is effective and focused on the goals
* **Author** - The developer that wrote the module/code that is being reviewed
* **Reviewer** - One or more developers that review the module

### Tools

* Crucible
* Gerrit
* FishEye
* Differential \(Phabricator\)
* Review Board
* Rietveld
* Barkeep
* CodeCollaborator
* TFS
* GitHub
* GitLab

