# IsaacLab-Task-Catalog-script


- The problem this script fixes:

* I generated an external project using the wizard project creator and now I want to run different tasks in it 
* However, my external project only runs RL-based tasks and only supports tasks that run on these libraries: (rl_games, rsl, skrl, ab3)
* I want to be able to import and run multiple tasks from the original IsaacLab project into my external project, but I don't know which tasks from the original project are supported by my external project. 
* How to figure out which other IsaacLab tasks can be run by my external project?
* Then how to figure out which run command to use for each?

- The solution:
. A script that outputs a table of supported tasks I can run on my project (according to the libraries I have in it)

- The way the script works is: it goes into the IsaacLab original project and reads the __init__.py file for each task there. It identifies which config entry points/config file addresses they have (config file addresses contain the names of the libraries they were written for). Then it goes into my external project, checks the names of all the script folders there (external projects are created by default with their script folder names containing the names of the libraries that they support) and matches them to the names in the original IsaacLab project config entry points. If there is no match, it flags as not supported. 
