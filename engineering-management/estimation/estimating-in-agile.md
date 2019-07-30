# Estimating in Agile

### **Estimating Size with Story Points**

{% hint style="success" %}
A **story point** is an abstract measure of effort required to implement a user story.
{% endhint %}

In simple terms, it is a number that tells the team about the difficulty level of the story. Difficulty could be related to complexities, risks, and efforts involved.

#### Scales

* Powers of 2: 1, 2, 4, 8, 16 …
* T-Shirt Sizing: X-Small, Small, Medium, Large, Extra-Large
* Fibonacci: 1, 2, 3, 5, 8, 13 …

However, it is tough to identify a story from the scales assigned to them. In order to do that each team would have to find a baseline story. It does not necessarily to be the smallest one, but the one that everyone within the team can resonate with. Once determined, sizing of all the user stories should be initiated by comparing them against the baseline.

While estimating story points, we assign a point value to each story. Relative values are more important than the raw values. A story that is assigned 2 story points should be twice as much as a story that is assigned 1 story point. It should also be two-thirds of a story that is estimated 3 story points.

### **Velocity** \(simple explanation\)

{% hint style="success" %}
**Velocity** is a measure of the amount of work a Team can tackle during a single Sprint and is the key metric in Scrum. Velocity is calculated at the end of the Sprint by totaling the Points for all fully completed User Stories.
{% endhint %}

{% hint style="info" %}
Story-Points per iteration = Velocity i.e. looking at past velocity estimate completion time of project \(use historical data if available or forecast or run one iteration\)
{% endhint %}

Points from partially-completed or incomplete stories should not be counted in calculating velocity. Velocity should be tracked throughout the Sprint on the Sprint Burndown Chart and be made visible to all Team members.

Velocity is a key feedback mechanism for the Team. It helps them measure whether process changes they make are improving their productivity or hurting it. While a Team's velocity will oscillate from Sprint to Sprint, over time, a well-functioning Scrum Team's velocity should steadily trend upward by roughly 10% each Sprint.

It also facilitates very accurate forecasting of how many stories a Team can do in a Sprint. \(In Scrum this is called using Yesterday’s Weather.\) For forecasting purposes the average of the last three Sprint's Velocity should be used. Of course, this means it takes three Sprints of experience for a Team to determine its Velocity accurately, which can sometimes be difficult to explain to impatient stakeholders.

Without Velocity, Release Planning is impossible. By knowing Velocity, a Product Owner can figure out how many Sprints it will take the Team to achieve a desired level of functionality that can then be shipped. Depending on the length of the Sprint, the Product owner can fix a date for the release.

### **Planning Poker, When to Play**

Planning Poker is a consensus-based estimating approach, it is most appropriate to use it on items that require consensus.

#### When to Play Planning Poker

_First_, a team should play Planning Poker after a meeting like a **story-writing workshop** in which they have written a large number of product backlog items. ****

This allows the product owner and team to identify a larger goal than can be achieved in one sprint, and create the user stories needed to reach the goal.

A typical quarterly story-writing workshop might produce 20 to 50 product backlog items. At a target rate of estimating about 20 items per hour, this could lead to two or so hours spent estimating for each quarter.

_The second_ time a team should play Planning Poker is once per sprint. Some teams will do this as part of a regular product backlog **grooming meeting**, and I think that’s fine if the whole team participates in grooming.

If the whole team does not participate, another good time to play Planning Poker is following one of the daily scrums late in the sprint. If the team estimates too early in the sprint, there’s a chance they’ll need to repeat the process for any late-arriving stories.

But the team should avoid estimating so late in the sprint that the product owner cannot consider the newly estimated items when deciding what the team will work on in the next sprint.

#### A Time Not to Play Planning Poker

There’s only one time when I think it’s a mistake to play Planning Poker: at the start of the **sprint planning meeting**. The first problem with doing it then is that it’s too late for the product owner to adjust priorities based on the new estimates.

Some product owners may be able to rejigger priorities on the fly, but even they could, probably do so better with a little more time to think.

A second problem with playing Planning Poker to start sprint planning is that it almost always causes the team to spend too much time estimating. 

### **When to re-estimate and Relative Size**

There are times when you want to re-estimate. Generally re-estimating is useful when you completely blew it on the original estimate and can see that the mistake was a rare occurrence. \(That is, if every estimate is systematically off by half I wouldn't re-estimate.\)

Second, you should re-estimate when there has been a change in relative size. For example, the team has discovered that learning AJAX will be about half as hard as they thought. We'd want to fix that because the new knowledge tells us that our relative estimates are off-kilter for the AJAX-heavy stories.

Relative estimation is the process of estimating task completion, not by units of time, but rather by how items are similar to each other in terms of complexity.

The Agile Alliance gives this definition:

{% hint style="success" %}
**Relative estimation** is one of the several distinct flavors of estimation used in Agile teams, and consists of estimating tasks or user stories, not separately and in absolute units of time, but by comparison or by grouping of items of equivalent difficulty
{% endhint %}

An example of relative estimation would be to say, "I think this feature is twice as complex as this other feature." There is no mention of time requirement, just that it is more complex than the other.

You may say that feature B  is "twice as complex" as feature A, which is a feature that you have completed. Because feature A took you three weeks, a reasonable guess for feature B would be six weeks!

### **Story Points vs. Ideal Days**

Traditional software teams give estimates in a time format: days, weeks, months. Many agile teams, however, have transitioned to story points. Story points rate the relative effort of work in a Fibonacci-like format: 0, 0.5, 1, 2, 3, 5, 8, 13, 20, 40, 100. It may sound counter-intuitive, but that abstraction is actually helpful because it pushes the team to make tougher decisions around the difficulty of work. Here are few reasons to use story points:

* Dates don’t account for the non-project related work that inevitably creeps into our days: emails, meetings, and interviews that a team member may be involved in.
* Dates have an emotional attachment to them. Relative estimation removes the emotional attachment.
* Each team will estimate work on a slightly different scale, which means their velocity \(measured in points\) will naturally be different. This, in turn, makes it impossible to play politics using velocity as a weapon.
* Once you agree on the relative effort of each story point value, you can assign points quickly without much debate. 
* Story points reward team members for solving problems based on difficulty, not time spent. This keeps team members focused on shipping value, not spending time. 

### **Cross-Functional team**

{% hint style="success" %}
A **cross-functional team** is a team in which the members have different skill sets, but are all working towards a common goal. It often includes people from different departments and from all levels of the organization, though it can also include participants from outside the organization.
{% endhint %}

These teams are usually **self-directed**. They are assigned tasks, which are then uniquely approached because of the various expertise of the team members. Each participant can offer their own perspective, leading to a more “out of the box” solution. This creative approach can lead to innovation, which can be a substantial market advantage over the competition.

Cross-functional teams often exist in **small or startup environments**. Because startups usually have a small number of employees, team members might have to perform a variety of tasks in different departments, thereby collaborating with those departments as well. This certainly creates a cross-functional team environment, even if the organization hasn’t acknowledged it yet.

Experts vary on whether these teams work best cooperatively or in competition or even both. Because members of cross-functional teams come from many different departments \(marketing, sales, finance, etc.\), they can subconsciously compete with each other by defending the interests of their core department. As far as the overall direction of a CFT, decisions can be made by consensus or by a team leader.

Cross-functional agile teams are common. If a cross-functional team mixes specialists from different fields, agile teams take this a step further. They make them combine and require each team member to expand beyond their area of expertise. Also, agile demands self-organizing teams, which dovetails nicely into the way a cross-functional team works.

