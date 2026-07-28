# IsaacLab-Task-Catalog-script

## Context
- The problem this script fixes:

  * I generated an external project using the wizard project creator and, during its creation, I selected the specific libraries it should be created with. Project Wizard only supports rl_games, rsl, skrl, ab3.
  * Now I want to run different tasks from the IsaacLab original project in my project.
  * However, my external project only supports tasks that run on the libraries that it was generated with but I don't know which tasks from the original project are supported by the libraries in my external project.
  * How to figure out which other IsaacLab tasks can be run by my external project ???
  * Then how to figure out which run command to use for each?

- The solution:
  * A script that outputs a table of supported tasks I can run on my project (according to the libraries I have in it)

## Prerequisites
* Have IsaacSim installed
* Have the original IsaacLab project from NVIDIA cloned to your local machine: https://github.com/isaac-sim/IsaacLab 
* Have an external project created with the Project Creator Wizard: https://github.com/marcelpatrick/create-a-new-external-isaaclab-project/blob/main/README.md 
  
## The way the script works :
  * it goes into the IsaacLab original project and reads the __init__.py file for each task there. It identifies which config entry points/config file addresses they have (config file addresses contain the names of the libraries they were written for). Then it goes into my external project, checks the names of all the script folders there (external projects are created by default with their script folder names containing the names of the libraries that they support) and matches them to the names in the original IsaacLab project config entry points. If there is no match, it flags as not supported. 

## How to Use it

1. Download this python script
2. Copy it inside your project folder `C:\Users\[YOUR USER]\[YOUR EXTRENAL PROJECT]\scripts\list_task_catalog.py`
3. Open Anaconda Prompt and activate your env: `conda activate [YOUR ENVIRONMENT]`
4. Navigate to your project folder: `cd C:\Users\[YOUR USER]\[YOUR PROJECT]`
5. Run with command: `python scripts/list_task_catalog.py`

## Task labelling

The script will return a table listing all tasks inside the original IsaacLab project from NVIDIA with two other columns: 
* Runnable in your Project?: classifies tasks into:
  * YES: Runnable by your current external project
  * NO: Not runnable by your current external project
  * NO — but supported by Project Wizard: Project Wizard can create projects with any of these 4 libraries (rl_games, rsl, skrl, ab3). Let's say that during project creation you only selected rl_games. If a task requires rsl, it cannot be run by your current project but you can create another project with Project Wizard, select rsl for that project, and run this task on that project. 
