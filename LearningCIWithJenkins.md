# Learning CI with Jenkins

## C01: Concepts of Continuous Integration

* Agile to the rescue
	The twelve agile principles
	* Customer satisfaction through early and continuous delivery of useful software. 
	* Welcome changing requirements, even late in development. 
	* Working software is frequently delivered (in weeks, rather than months). 
	* Close daily cooperation between businesses, people, and developers. 
	* Projects are built around motivated individuals, who should be trusted. 
	* Face-to-face conversation is the best form of communication (co-location). 
	* Working software is the principal measure of progress. 
	* Sustainable development—able to maintain a constant pace. 
	* Continuous attention to technical excellence and good design. 
	* Simplicity—the art of maximizing the amount of work not done—is essential. 
	* Self-organizing teams. Regular adaptation to changing circumstances.
	** from [Agile principles](http://www.agilemanifesto.org)**
	
* The Scrum framework
	* Important terms
		* **The Sprint**: Sprint is a timebox during which a usable and potentially releasable product gets created. A new Sprint starts immediately after the conclusion of the previous Sprint.
		* **Product Backlog**: The Product Backlog is a list of all the required features in a software solution.
		* **Sprint Backlog**: The Sprint Backlog is the set of Product Backlog items, selected for the Sprint.
		* **Increment**: The Increment is the sum of all the Product Backlog items completed during a Sprint and the value of the Increments from all the previous Sprints.
		* **The development Team**: The Development Team does the work of delivering a releasable set of features named Increment at the end of each Sprint.
		* **The Product Owner**: The Product Owner is a mediator between the Scrum Team and everyone else.
		* **The Scrum Master**: The Scrum Master is responsible for ensuring Scrum is understood and enacted. Scrum Masters do this by ensuring that the Scrum Team follows the Scrum theory, practices, and rules.
	* How does Scrum work?
		* Sprint Planning: Sprint Planning is an opportunity for the Scrum Team to plan the features in the current Sprint cycle.
		* Sprint cycle: the developers simply work on completing the backlogs decided in the Sprint Planning.
			* Daily Scrum meeting: During the Scrum meeting, the Development Team discusses what was accomplished yesterday, and what will be accomplished today. They also discuss the things that are stopping them from achieving their goal. The Development Team does not attend any other meeting or discussion apart from the Scrum meeting.
			* Monitoring Sprint progress: The Daily Scrum is a good opportunity for a team to measure its progress.
		* Sprint Review: the Development Team demonstrates the features that have been accomplished. The Product Owner updates on the Product Backlog status to date.
		* Sprint Retrospective: In this meeting, the team discusses the things that went well, and the things that need improvement. The team then decides the points on which it has to improve to perform better in the upcoming Sprint. This meeting usually occurs after the Sprint Review and before the Sprint Planning.

* Continuous Integration
	* CI: is a software development practice where developers frequently integrate their work with the project's Integration branch and create a build.
	* Agile runs on CI: The Agile software development process focuses mainly on fast delivery, and CI helps Agile in achieving that speed.
		- Develop & Commit => Build with notification => Integration with notification => Build on Integrated code with notification => Integration testing with notification => Packaging
	* Types of projects that benefit from CI
		- Smart device's software
		- Web-based projects
		- mobilte phone apps

* Elements of CI
	* Version control system: A Version Control System, sometimes also called a Revision Control System, is a tool to manage your code history.
	* Branching strategy: A CI tool is at the center of the CI system, connected to the Version Control System, build tools, Binary Repository Manager tool, testing and production environments, quality analysis tool, test automation tool, and so on.
	* GitFlow branching model
	* CI tool: What is a CI tool? Well, it is nothing more than an orchestrator. A CI tool is at the center of the CI system, connected to the Version Control System, build tools, Binary Repository Manager tool, testing and production environments, quality analysis tool, test automation tool, and so on.
		* A CI tool provides options to create pipelines. 
		* Each pipeline has its own purpose. There are pipelines to take care of CI. Some take care of testing; some take care of deployments, and so on. 
		* Technically, a pipeline is a flow of jobs. Each job is a set of tasks that run sequentially. 
		* Scripting is an integral part of a CI tool that performs various kinds of tasks.
		* the script is getting replaced by the growing number of plugins available in Jenkins.
	* **Self-triggered builds**
		* The self-triggered automated build is the most important part of a CI system.
		* The build automation can take the help of build tools like Ant and Maven.
	* Code coverage：Code coverage is the amount of code (in percentage) that is covered by your test case.
 	* Static code analysis: Static code analysis, also commonly called white-box testing, is a form of software testing that looks for the structural qualities of the code.
	* Automated testing: However, automating the testing process is a bit more difficult than automating the build, release, and deployment processes. It usually takes a lot of effort to automate nearly all the test cases used in a project. It is an activity that matures over time.
		* SIT: System Integration Test
		* UAT: User Acceptance Test
		* PT: Performance Test
	* Binary repository tools: 
		* A binary repository tool is a Version Control System for binary files.
		* Along with managing built artifacts, a binary repository tool can also manage 3-party binaries that are required for a build.
	* Automated packaging: The task of creating a single archive or a single media out of many components is called packaging. 
	
* Benefits of using CI
	* Freedom from long integrations
	* Metrics
	* Catching issues faster
	* Rapid development
	* Spend more time adding features

* Summary
> Behind every successful agile project, there is a Continuous Integration process

** Code Coverage**  

| Type of coverage  | Description |
|  ----------------- | ------------|
| Function | The number of functions called out of the total number of functions defined |
| Statement | The number of statements in the program that are truly called out of the total number |
| Branches |  The number of branches of the control structures executed |
| Condition | The number of Boolean sub-expressions that are being tested for a true and a false value |
| Line | The number of lines of source code that are being tested out of the total number of lines present inside the code. |

## C02: Installing Jenkins

### Running Jenkins inside a servlet container

### Installing a standalone Jenkins server on Windows

### Installing a standalone Jenkins server on Ubuntu

### Installing a standalone Jenkins server on Red Hat Linux

### Running Jenkins behind a reverse proxy

### Running Jenkins on Docker

## C03 The New Jenkins

* The Jenkins setup wizard
	* You can always log in to Jenkins using the password from the  ```intialAdminPassword``` file and the username ```admin```.


### The new Jenkins pipeline job
The concept of Pipeline as Code rethinks the way we create a CI pipeline. The idea is to write the whole CI/CD pipeline as a code that offers some level of programming and that can be version controlled.

* create pipeline, click on the **try sample Pipeline...**, select **scripted pipeline**.

* Set JAVA_HOME
	* Go to Jenkins -> Manage Jenkins -> Configure System -> Global properties Check the box 'Environment variables' and add the JAVA_HOME path

### Declarative Pipeline syntax
The Declarative Pipeline syntax is a more simplified and structured version of the Groovy syntax.
* node
	* A node block defines the Jenkins agent wherein its constituents (stage blocks, directives, and steps) should run.
* stage
	* A stage block is a collection of closely related steps and directives that have a common objective.
* directives
	* The main purpose of directives is to assist the node block, stage block, and steps by providing them with any of the following elements: environments, options, parameters, triggers, tools.
* steps
	* Steps are the fundamental elements that make up the Declarative Pipeline. A step could be a batch script or a shell script, or any other command that's executable.

### Jekins pipeline syntax utility

### Jenkins Blue Ocean
This chapter should be spent more time.

## C04: Configuring Jenkins


## Resouce
[The source code in git](https://github.com/PacktPublishing/Learning-Continuous-Integration-with-Jenkins-Second-Edition)