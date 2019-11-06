# sdlc-redux
API-driven reimagining of the SDLC (Solution Delivery Lifecycle) process

## A little domain-driven design (**DDD**)...
Let's consider the domains in play in the SDLC.
1) Users - the people who will be participating in the process
2) Roles - the various roles the *Users* will assume throughout the process
3) Artifacts - the various work products that are produced throughout the process
4) Releases (aka, Solution Releases; Product Releases) - a defined collection of Artifacts which ultimately results in a Solution getting deployed into production; Releases undergo various stages (states) of the lifecycle
5) Stages - the defined checkpoints that a Release should undergo in the SDLC on its way to production deployment

The domain model should look something like the following:


```
      +------+        +------+
      | User |  <---- | Role |  
      +------+        +------+
          |
          |
          V
      +----------+           +---------+            +---------+  
      | Artifact |  ------>  | Release |   <-----   |  Stage  | 
      +----------+           +---------+            +---------+


```
__Relationships__

- A _User_, identified with a unique identifier, will have one or more _Role_

- _Roles_ include ArtifactProducer, ArtifactApprover, ArtifactReviewer, ReleaseReviewer, ReleaseOwner, ReleaseApprover 

- An _Artifact_ is produced by a _User_; an _Artifact_ also has one or more _Users_ who are Reviewers and Approvers

- A collection of _Artifacts_ constitute a _Release_

- A _Release_ transitions through _Stages_ in the lifecycle; a given _Release_ can only be in one _Stage_ at any given time; the _Release_ should have a required minimum set of _Artifacts_ at a given _Stage_

- _Stages_ are somewhat nebulous; the following should work for both Agile, Iterative, and Waterfall style deliveries: 
  - Inception
  - DevTest
  - Verification/Validation
  - Production

\_**Comment**\_: The _Stage_ "DevTest" is little bit difficult for an Agile _Release_ (or Increment), because it consists of multiple Sprints. The current plan is to define one or more _Artifacts_ that define an individual sprint, and have an approval process for the sprint-level _Artifacts_.

Looking at the current domain model, it all looks rather simplistic! The devil, I guess, will be in the details.
