---
layout: post
read_time: true
show_date: true
title:  Microsoft Techdays Paris 2013 - Day 2
date:   2013-03-20 08:00:00 +0100
description:  Microsoft Techdays Paris 2013 - Day 2
img: posts/uncategorized/microsoft.png
tags: [TechEvents]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/microsoft-techdays-paris-2013-day-2.html'
---

The theme for second day is more about ALM, TFS and Agile.

### Session 1: ALM as a Service with TFS (OBS IT&Labs)

**Global objectif:** 
- professionalisation
- coherence: shared best practices, code rules etc
- unification

<!--more-->

**Working principle:**
- DSI manage TFS Server which includes project collections
- Departement manager manage project collection
- Project leader manager team project

**Tools:**
- Team System Web Access portal is userful as a tool for Application Lifecycle Management.
- TFS Administration tools is a tool for managing user rights.

**Team Project templates**: Scrum, Agile, CMMI

### Session 2: Agile Patterns with VS 2012 and TFS 2012 (MediaPost, Cellenza)

**Scrum principles:**
- Non-negotiable Quality
- Business oriented
- Rapide delivery

**Scrum actors:**
- Scrum master:
Has no management authority

Doesn't have a project role

Facilitator, protect the team from distraction

- Product owner: project manager
    - Resposible for ROI(return on investment)
    - Final arbiter of requirement questions
    - Focused more on the what than on the how

- Scrum Developmer Team: analyse backlog, develop and deliver product
    - Crosse-functional group
    - Attempts to build a "potentially shippable product increment" every sprint
    - Collaborates
    - Self-organizing
    - Small team more often from 4 to 9 people

Terms:
- PBI: Product Backlog Item
- PO: Product Owner

Agile ALM Tools: Collabnet Teamforge

Scrum has three **artifacts**: 
- Product Backlog
- Sprint Backlog 
- Burndown Chart

**Scrum board**: Story->To do->In Process->To Verify->Done

Product Backlog: List of all the items in one application and ordered by priorities from high to low

Sprint Backlog: What we have agreed to do during the current sprint


**Scrum meetings(ceremonies):**
- Planning poker
- Sprint planning meeting
- Daily scrum (iterates): what have been done, what have to do today, what difficulties have been met
- Sprint review meeting(demo): scrum dev team show shippable product to the product owner and other related persons.
- Sprint Retrospective meeting(bilan): what went well, what could be improved, feedback

Backlog refinement meeting is paralleled.

Backlog refinement meeting: divide big items into several small items

Backlog Refinement meeting can be called: Product Backlog Grooming or Backlog Estimation or Story Time

The most important objectif of backlog refinement meeting is get better understanding of the upcoming work and split it into small items
- Estimation of efforts
- Clarification of effort
- Decomposition of large tasks into small ones

**Sprint Characteristics:**
- Independent
- Negotiable
- Valuable
- Estimable
- Small
- Testable

**Sprint Planning Meeting:**
- A sprint should include analysis, design, implementation, testing, integration and deployment.
- A 30-day sprint uses 1 day for sprint planning meeting
- A two-week sprint use 4 hours for sprint planning meeting

**Definition of "done" in a sprint:**
- properly tested
- refactored
- potentially shippable

only **60%** of the tasks are likely to be identified during the sprint planning meeting. 

Other tasks, such as unanticipated dependecies, will be discovered during sprint execution.

Each sprint is an iteration, it includes: evaluation & priorization, detailed requirements, design & analysis, implementation & developer testing, acceptance testing, deployment

**Agile Benefice:**
- Visibility of realized work by the team
- Coherence between the tools and methods
- Reduction of time for PO(product owner)

**Daily Scrum meeting:**
- 15 minutes each day
- PO can attend or not attend daily scrum

A sprint task good size is one person-day task, so than other team member can detect whether a task is stuck

TDD is not a part of Scrum

TDD principle: write failed test  -> write successful product code -> refactor code -> repeat the same operation

#### Who will be responsible for tool selection and configuration for Agile methods? 
Answer: the team

#### When is sprint execution completed?
Answer: when the timebox expires

Sprint review meeting:
#### The first thing should see at the sprint review meeting?
Answer: live demonstration of a potientially shippable(properly tested) product increment

#### The stackholder complains to who directly?
Answer: product owner

#### What's the best time with sprint review meeting to discuss feedback from outside stakeholders?
Answer: the end; after the demonstration and measurement of which goals have achieved

#### If we keep the product visible and encourage open communication, will the product backlog usually get bigger or smaller over time?
Answer: The product backlog will grow because people ask for things in response to what they've seen

Sprint Retrospective meeting:
- 1) Safety check

#### Is retrospective safety enchanced by inviting outside spectators who weren't working on the team?
Answer: No. If the team needs to discuss issues with outsiders it's usually better to do this after the retrospective

#### Is a safety check by itself a complete sprint retrospective?
Answer: No.

- 2) Classic scrum retrospective
    - What went well 
    - what can be improved

#### In scrum, how often is the sprint retrospective meeting conducted?
Answer: Every sprint

- 3) focused conversation principles
    - Objective questions(what happened?)
    - Relective questions(how do we feel about it?)
    - Interpretive questions(what does it mean?)
    - Decision questions(what are we going to do about it?)
- 4) silent writing
- 5) timeline retrospective
- 6) decisions

References:
- https://scrumtrainingseries.com/
- http://www.collab.net/services/training/agile_e-learning


### Session 3: TypeScript for dummies (MCNEXT)

TypeScript is a language for application-scale JavaScript development.

TypeScript is a typed superset of JavaScript that compiles to plain JavaScript, it's 100% compatible with JavaScript

Any browser. Any host. Any OS. Open Source.

TypeScript compiler is a console application.

TypeScript extension is .ts

Example:

- 1) variable:
```typescript
var toto :Any = 12;
var toto :number 
var toto :int
```

- 2) function
```typescript
function mymethod(x:bool, y:number){...}
```

- 3) optional parameter
```typescript
function mymethod(k?:string, l:number=10){...}
```

- 4) export class

- 5) method override:
```typescript
modifier()
modifier(poid:number)
modifier(k?:Any)
```

- 6) arrow function

- 7) casting

- 8) ambient declaration
```typescript
declare var $; (it doesn't generate javascript code)
```

- 9) reference to files
```typescript
///<reference path="...ts" />
```

### Session 4: ALM & e-commerce, le challenge continu! (SOGETI)

A big team project is recommended!

user right is controled 

Checkin policy:
- comment mandatory
- work item mandatory(commit attached to work item)
- personalized policy
- observation

I hope this post can do help!

Enjoy coding!