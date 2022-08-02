# Occasional Retrospective Notes

## Tuesday 2-Aug-2022

Lots of little work done on the Bigfoot WL Bib Record Form project [here](https://github.com/nojronatron/Bigfoot-Bib-Report-WL-Form), and some pretty good collaboration started with a small group of 4-5 others. Success for this iteration of the form looks promising!

Yesterday I spent several hours reviewing bogposts and freebie articles about interviewing. Turns out a lot of my fears about interviewing are not really justified, and my *approach* to interviewing is what needs to be adjusted. An adversarial interview is not what anyone is looking for (if they are serious about filling a position, or on the flip side earning an offer to fill a position). Instead, my view needs to focus on researching the company and the position I am interested in, and during the interview use that information to help inform my responses. The research should also answer lots of questions about a company and the position but it cannot possibly answer them all, so I should bring those remaining questions to the interview with me, and learn what I can while I have the *inside opportunity to ask them*. There is opportunity on both sides, and I need to leverage this to help me have positive interviewing experiences, regardless if an interview turning into an offer.

Over the weekend I began working on a collaboration project with Ryan S in Bellingham. We agreed to work on a mern-stack project, basically rewriting a project I already have underway using DotNet. We are both looking to gain more experience with most (if not all) aspects of software development, but especially javascript, react-js, node, and probably express-js and mongo. We will also benefit from utilizing common software management tools like GitHub and Trello, and following some good practices to plan-out this project. Also, there is already a 'customer' for this project, so I suspect we will some experience with engaging with a client and honing the project to a real use-case. I'm looking forward to working with Ryan, and moving this project forward!

These last few days I learned about:

- GitHub Release zipping process does not maintain CRLF in plain text files, only LFs used which can be an issue for some apps or environments.
- CircleCI has a free tier that can be helpful to manage build and release processes, integrated with GitHub (thanks Jason Martin for the tip!).
- CSS can be fun, if appropriate challenged. Kyle on YouTube at [Web Dev Simplified](https://www.youtube.com/c/WebDevSimplified) turned me on to [CSSBattle](https://cssbattle.dev) so I have yet another diversion, but this might pay-off when it comes to my upcoming collaborative project with Ryan, revamping [LingoBingoGen](https://github.com/nojronatron/LingoBingoGen).
- Adding badges to a readme.md file isn't too tough. Check out [shields.io](https://shields.io) for tools to build common or custom badges.
- Preparing for an interview takes a bunch of time, but understanding that the goal is to learn about the company and team, and allow them to learn about you (the candidate) is ultimately what is required to discover if the position and the candiate are a good fit.

## Friday 29-July-2022

At some point in the future, I'll want to change-up this format to something like a more formal blog article. I haven't decided yet what it will be, other than not a massively long MD file with a FILO stack of entries.

I finished up the Zip Linked Lists code challenge review by performing a mock whiteboard interview within a 45 minute period and then adding the whiteboard to the solution. This is not really sustainable in that it will cause a tremendous number of repositories to appear in my GH profile with little benefit (to anyone), so I plan to set up separate code challenge repositories for various languages.

Related, I worked my way through a CodeWars challenge in javascript (which I haven't written much of lately). I followed the general rubrik outlined by Code Fellows for a technical interview and produced reasonable code that passed the default CodeWars unit tests. Not that that is everything! So this prompted me to create a new js-specific code challenge repository, so this a future efforts will have a place to live.

Somehow I decided today was a good day to look up how to add emojis to markdown files. There are at least two ways:

- If supported, just use colon-surrounding syntax i.e. `:smile:`
- Point to the appropriate API using image placeholder syntax i.e. `![smiley](url-to-smiley-emoji)`

For example:

`:smile:` in supported markdown interpreters results in a :smile:

`!["smiley"](https://github.githubassets.com/images/icons/emoji/unicode/1f603.png?v8)` results in a vvv large smiley vvv

!["smiley"](https://github.githubassets.com/images/icons/emoji/unicode/1f603.png?v8)

Here are a couple of references with more info:

[Emoji Cheat Sheet](https://github.com/ikatyang/emoji-cheat-sheet#smileys--emotion)

Markdownguide.org's [Extended Syntax guide](https://www.markdownguide.org/extended-syntax/#overview)

## Thursday 28-July-2022

Building Java Projects in GitHub using GH Actions. There is a template in github repo 'actions/starter-workflows' that is a good starter. Originally I copied an existing yml file from a CodeFellows example, but that was designed for a slightly different environment and project, so I had to modify it. There were a couple issues:

1. gradlew could not be found. This was probably because I was forcing a CHDIR in the yml file and I didn't need to.
1. gradlew could not be executed. In Linux, file permissions are managed using bits for Read, Write, eXecute, etc. Windows does as well but it is a little different. In my yml I defined an Ubuntu environment for building and testing, so permissions could be a problem. Git has the ability to set permissions via `git update-index --chmod=` and to add eXecute permissions append `+x` to the end.
1. The last change that was required was to set the JDK compatibility level to 11, instead of 17 (not supported in GH Actions?).

Earlier today was a Code 401 instructor's panel where they discussed current content in those classes. There was a good amount of discussion around C#/DotNet, and TypeScript (which is starting to make inroads to the JS class due to increased use in the industry). There was also good discussion around strategies to deal with learning to code, especially JS, such as breaking down the problem in words, and writing solutions as comments rather than code, and then worry about coding the problem once an algorithm appears to solve the problem at hand.

## Wednesday 27-July-2022

Today I passed the final technical interview at Code Fellows and am officially an alum! Certificate is due in a week or so!

Passing the technical interview was extremely difficult, and I followed the advice I'd received from Code Fellows instructors and staff: Stick with it, pay attention to the details, break down a problem into the smallest parts, and take care of myself along the way. I will continue to do more technical interview practicing while I job hunt, so that I am well practiced and can more easily get over nervousness during a real interview.

Today I picked-up where I left off with one of my older projects, the [Bigfoot Bib Report WL Form](https://nojronatron.github.io/Bigfoot-Bib-Report-WL-Form/). The BigFoot 200 event is coming up and during a recent preparatory meeting the form was re-introduced (much to my surprise and delight) and there was new (and renewed) interest in it. I'm going to try and get this as ready as possible, with help from other interested volunteers to test it and provide feedback on possible improvements.

There are a ton of projects on my pet-project kanban board that I stil need to get to. There is definitely more work than there is time. At least these projects and tasks are centered around the goals of improving my software developer skills in every regard, and prepare me for my next big thing.

## Footer

Back to [root README](../README.md)
