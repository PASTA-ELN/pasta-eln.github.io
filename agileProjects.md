# Agile Project Planning

## Motivation
One of the inspirations for PASTA was the agile project management for IT-projects [https://en.wikipedia.org/wiki/Scrum_(software_development)]. We believe that **agile project planning** is also highly beneficial for scientific research projects. Here, we briefly talk about how PASTA-ELN can be used for agile project planning.

## Structure of projects
PASTA uses a hierarchy in its datastructure and on the hard disk which is inspired by SCRUM:
1. projects have
  - a name: e.g. Peter_Tribology
  - a objective/goal (paper, thesis *writing*, baked cake) [optional]
  - a status [paused, active, finished]
2. steps, sprint:
  - should have mini-objectives
  - in SCRUM-projects it is in between one meeting and next
  - by default, they are called task to make it easier for beginners
3. subtasks
  - the smallest level in the default configuration
  - in SCRUM-projects it is specified by the worker,

Benefits of this hierarchical local folders and projects are:
  - programs can efficiently process it
  - other people/supervisor can collaborate
  - do not only exchange .pptx presentations but data, meta-data, and information

This could result in a project directory that looks like:
- 00\_Experiment_Instrument1
- 01\_Experiment_Instrument2
- 02\_Analysis
- PAPER
- TALK


## Meetings
If you subscribe to the SCRUM-framework, you can use the comment of the task/subtask as an area to store your meeting notes. An advanced editor allows you to add structure to the notes

According to SCRUM, meetings
- occur at the end of every sprint, e.g. biweekly
- finish sprint, reflect sprint, plan a new sprint
- specify measurable goal at the beginning of a sprint
  - what is desired during the sprint
  - should be prepared by the scientist
- identify easy and difficult tasks: pushed forward, backward
- "Tasks" list of to-dos

## Details
### Projects
- includes the objective of the project
- with tags (e.g. #FEM #EBSD)
- have a state: active, passive, paused, ended

### Steps, Tasks
- arbitrary names
- can use operating procedures, samples, ...

### Software projects that are stored in PASTA
this project is a software project that is stored in PASTA
- step/task text has progress report and future features
- documentation can be a part of the hierarchy. It can be a task to produce "Documentation" that can be uploaded to a separate repository as [git-submodule](http://git-scm.com/book/en/v2/Git-Tools-Submodules)
- even the source code could part of the project and uploaded in a separte repository.
- The inclusion of submodules is currently not implemented.
