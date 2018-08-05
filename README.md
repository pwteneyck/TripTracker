# TripTracker
A solution for tracking/managing group travel

## Motivation
Coordinating group travel involves a number of moving pieces. Plane tickets and other transportation, local transportation such as rental cars, taxis, Uber, etc., travel insurance, and more, all need to be taken into account and managed. When a church or other ministry decides to manage short-term missions trips, a host of new considerations are added: support-raising, trainings, an application pipeline, coordinating with local ministries, gathering necessary supplies, and communicating all of these needs to individual trip participants becomes a time-consuming process. For larger organizations that send multiple trips each year, this process becomes a full-time job.

Currently, no dedicated software solution exists to aid the coordinator in their role. Existing options such as ManagedMissions and Church Community Builder offer some tools that fit the use cases of coordinating group travel, such as the ability to track funds raised and easily communicate with specific groups of people, but leave many processes, such as tracking forms, trainings, and budgets across multiple trips, up to the coordinator. Alternatives to specialized software - typical organizational solutions like Airtable, Asana, or G Suite - allow much more flexibility for coordinators to build tools that meet their needs. However, because at the end of the day these tools are *just tools*, many solutions built there end up being "better than what we had before" and don't meet every need any more than managed solutions do.

As organizations grow and expand their missions efforts, an effective software solution that ties together tools to meet the many different needs of trip coordinators becomes more important. Such a solution has two main benefits:

1. **Minimize manual tasks:** Increasing the scope of the software used by a human being reduces the ability of that person to make mistakes: typing incorrect email addresses, accidentally sending out a link to a church-wide budget spreadsheet instead of a training schedule, or attributing donations to the wrong user are all honest mistakes that can be avoided by the use of software. As an organization grows to manage more and more concurrent trips the risk of user error grows proportionally, but the risk of software error remains (relatively) constant.
1. **Increase efficiency:** Software designed to meet the needs of a trip coordinator reduces the amount of work needed on their part to see a trip through from start to finish. This allows a coordinator to manage more trips than they would using a different, non-specialized tool (or collection of tools), and also allows for easier collaboration between a team of coordinators.

## Goals
This software (it needs a name that's catchier than "TripTracker") should manage the relational aspect of all of the data behind mission trips. It should:

* handle as much of the administrative overhead of coordinating short-term trips as possible, eliminating completely the need for repetitive manual processes. 
* Be inexpensive to operate and maintain. 
* Manage identities of coordinators and trip participants.
* Track action items for trips (e.g. booking plane tickets) and for individuals (collecting medical information or trip applications).
* Allow for easy communication (send a form email to all trip participants or all leaders).
* Provide a tiered authorization scheme, allowing different people access to different information (trip leaders can see funds raised for their team members but not for other trips, while non-leaders can only see their individual support raising progress).

## Architecture
*(Work in progress)*

The application should consist of three main layers: a front-end UI accessed through a web browser or (further down the road) a mobile application, a REST service exposing the various APIs necessary for tracking and coordinating trips, and a persistence layer storing all of the necessary data.

This application will be provided as a library, not as a managed solution (there's no one to manage it, currently), meaning that any organization choosing to use this application would fully own its own stack. With this in mind, the application should be written in a relatively modular way, to allow users to support any persistence layer they want to use. 

The REST service, then, consists of two components: a routing/logic layer which handles requests from the UI and a data-access layer which serves as an adapter to the persistence layer. For ease of use, the application should include at least one template (such as an [AWS CloudFormation template](https://aws.amazon.com/cloudformation/aws-cloudformation-templates/)) and matching adapter to use out-of-the-box.

The user would also be responsible for hosting the application (REST service and UI). Again, this means that the REST service should be written in as platform-agnostic of a way as possible and that any resource templates included in the initial library should include resources for deployment (such as AWS CodeDeploy and Lambda/EC2).
