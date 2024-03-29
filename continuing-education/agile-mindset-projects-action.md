# Agile Learning Notes

## MSFT Learning - The Agile Philosophy

Emphasizes:

- Incremental delivery
- Team collaboration
- Continual planning
- Learning

Based on iterative development.

### Vertical Teams

Horizontal teams tend to have a structure similar to the project they are working on: UI, back end, etc.

Vertical teams "span the architecture and align with product outcomes".

- Members with skill sets that cover all areas to complete the feature come together as a team.
- Scaling occurs by adding teams, rather that building the organization of a single team.

### Azure Boards

Create an agile Kanban style board:

1. Create a Project
2. Create a Team
3. Add Team members
4. Create the board
5. Define a sprint
6. Assign tasks and set the iteration

### Several Processes

Agile development can be done following several processes:

- Agile: Scales well for many team and project sizes
- Scrum: Requires a Scrum Master with expertise in Scrum, and a team with Scrum training
- CMMI: For very large teams and/or projects that is much more complicated and usually overboard for smaller projects

## Microsoft Reactor Agile Mindset

Host: Sandy Liu, Certified Scrum Master

### Agile Mindset

What is Agile?

- SDLC development, integrations, etc
- Product requirements, analytics, etc
- Management such as Kanban, Scrum, etc
- Manifesto: Empowerment, collaboration, etc

### Manifesto

circa 2001

12 values and principals

This presentation will focus on the values:

- Individual and team interactions
- Working software
- Customer collaboration
- Responding to change

See the manifesto for the full context, because the values are not isolated, nor are they hard-and-fast rules.

### Mindset Values Principles Practices

Mindset:

- Developed and cultivated over time
- Just 'acting agile' is not equivalent to understanding and executing in an agile way
- Prioritizes Unity: Shared knowledge, open communication, disarmed environment
- Working solutions: Iterative, small-incremental value returns
- Customer Focus: Understand and meet needs of users
- Flexibility: Respond quickly and effectively to change and new ideas

Note: See the signatories of the Agile Manifesto for insight into who they are and what they stand for.

Values:

- People and conversations should be valued over utilizing processes and tools
- Complicated workflows are often a sign of an attempt to avoid communication and collaboration
- Celebrate new ideas and improvements from conversations lead to innovative thinking
- Focus on producing working software over comprehensive documentation
- Documentation should be focused on _executable_ units of work
- Know your customers (internal and external), check in with them for feedback loops and to build trust
- Focus on _value driven delivery_, and get them out early-on in the project

Note: Change is hard and uncomfortable, however pivoting is necessary to being able to continue delivering value. Adapting and adjusting to the environment will lead to success.

Culture: A critical component of an Agile mindset.

### Organizational Culture

Encompass values and behaviors that teams adhere to.

Develop software in better ways by:

- Doing it (yourself, as a team)
- Helping others to do it (teach and learn)

Team Effort:

- What can I learn? How can I help make things better?
- Skills, knowledge, and processes are not guaranteed to translate from team to team

Creating successful culture needs (in order of importance):

1. Psychological safety
2. Meaningful work
3. Feeling of personal impact
4. Sructure and clarity
5. Dependability of team members

There is an idea of Radical Candor _[Radical Candor, by Tim Scott]_

Radical Candor is:

- Respectful confrontation.
- Trust.
- Fundamental change.
- Challenging directly.
- Caring personally.

Common fears:

- Being truthful about bad news
- Making mistakes
- Speaking up
- Adminitting blockers
- I don't know
- Asking for help
- Questioning or challenging ideas and opinions

Lack of seeing these fears could mean a lack of innovative, collective, agile performance.

## Delivery Plans

How delivery plans enabled teams to plan, schedule, and coordinate work:

- Present a calendar view with work items and dependencies.
- Call-out dependencies across Sprints and Teams, highlighting delivery schedule conflicts.
- Enable moving Work Items to handle dependency conflicts quickly and easily.

Create a delivery plan and optimize sprint workload for delivery efficiency:

- Use the Azure DevOps administration console.
- Create a new Project or use an existing one.
- Create a Team or use an existing one.
- Create a New Plan for the Project and provide a Name, Backlog Items backlog, and add your Team.

View dependencies within work items in one/across teams:

- Use the Delivery Plans view.
- Notice the Red and Green link icons.

Resolve dependencies that have issues:

- Red Link icons indicate dependency issues.
- Overlapping delivery dates will cause dependency issues.
- A predecessor Work Item with a delivery date later than a successor will cause a dependecy collision.

### What Delivery Plans Are

Visualization of one or more work schedules against a calendar backdrop.

Provides teams and mgmt with over view of plans to produce and when.

Must be occasionally synchronized with other teams' schedules.

Like a calendar with Sprint swimlanes, icons indicating dependencies between work items, and Milestones.

Multiple teams are displayed so Sprints and Swim Lanes can be lined up.

There is _no focus_ on the logistics of how deliverables will be produced.

### How To Set Up Delivery Plans

1. Sign In to the Azure DevOps.
2. Create a new project by selecting a template and provide a name and select your Azure DevOps Organization.
3. Click Create Project.
4. Navigate to the project in Azure DevOps.
5. Select Delivery Plans under Boards.
6. Click New Plan.
7. Provide a Name, Backlog Items backlog, and add the Team.
8. Click create.

### Schedule Milestone Markers

Add these as reference points to help plan work within context of significant or extenral dates.

Add a Date, Label, and Color to the markers for visibility.

### Optimizing the Work Schedule

Green Links indicate linked dependencies.

Red Links indicate depedency conflicts.

Find Work Items with Dependency conflicts and reorganize them as appropriate.

Work Items with overlapping or swapped due dates should be dragged between Sprints to ensure an item is not blocked by another team or Work Item.

Ensure that predecessor work items dates do not overlap with successor work item dates.

### Considerations when scaling Agile Efforts

Build trust in people and processes.

Elevate the organization above the team and the individual.

Foster a culture of transparency.

## Takeaways

Agile Framework is not about Scrum or Kenban methodologies.

Don't just go through the Agile Methodology motions.

## Resources

Confessions of a Scrum Master (Amazon)

Radical Candor, by Tim Scott

The [Agile Manifesto](https://agilemanifesto.org/?azure-portal=true)

Microsoft Learn Modules: [Get Started With Azure Devops](https://learn.microsoft.com/)

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
