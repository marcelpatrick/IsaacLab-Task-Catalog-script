# IsaacLab-Task-Catalog-script

## Context
- The problem this script fixes:

  * You cloned NVIDIA's [IsaacLab](https://github.com/isaac-sim/IsaacLab) original project to your local machine. It comes with several tasks. P
  * You generated an external project using the [Wizard Project Creator](https://github.com/marcelpatrick/create-a-new-external-isaaclab-project/blob/main/README.md ) and, during its creation, you selected the libraries it should be created with from a list of supported ones (project Wizard only supports rl_games, rsl, skrl, ab3).
  * Now you want to run different tasks from the IsaacLab original project inside your external project.
  * However, you don't know which tasks from the original project are supported by the libraries in your external project.
  * How to figure out which IsaacLab tasks can be run by your external project ???
  * Then, how to figure out which run command to use for each?

- The solution:
  * A script that outputs a table of tasks you can run in your project with their respective run commands.

## Prerequisites
* Have IsaacSim installed
* Have the original IsaacLab project from NVIDIA cloned to your local machine: https://github.com/isaac-sim/IsaacLab 
* Have an external project created with the Project Creator Wizard: https://github.com/marcelpatrick/create-a-new-external-isaaclab-project/blob/main/README.md 
  
## The way the script works :
  * it goes into the IsaacLab original project and reads the __init__.py file for each task there. It identifies which config entry points/config file addresses they have (config file addresses contain the names of the libraries they were written for). Then it goes into my external project, checks the names of all the script folders there (external projects are created by default with their script folder names containing the names of the libraries that they support) and matches them to the names in the original IsaacLab project config entry points. If there is no match, it flags as not supported. 

## How to Use it

1. Download this python script
2. Copy it inside your `scripts` folder inside your external project: `C:\Users\[YOUR USER]\[YOUR EXTRENAL PROJECT]\scripts\list_task_catalog.py`
3. Open Anaconda Prompt and activate your env: `conda activate [YOUR ENVIRONMENT]`
4. Navigate to your project folder: `cd C:\Users\[YOUR USER]\[YOUR PROJECT]`
5. Run command: `python scripts/list_task_catalog.py`

## Task labelling

The script will return a table listing all tasks inside the original IsaacLab project from NVIDIA with two other columns: 
* Runnable in your Project?: classifies tasks into:
  * YES: Runnable by your current external project
  * NO: Not runnable by your current external project
  * NO — but supported by Project Wizard: Project Wizard can create projects with any of these 4 libraries (rl_games, rsl, skrl, ab3). Let's say that during project creation you only selected rl_games. If a task requires rsl, it cannot be run by your current project but you can create another project with Project Wizard, select rsl for that project, and run this task on that project. 

## WHAT THIS SCRIPT DOES NOT DO
 
It does not train, does not launch Isaac Sim, does not touch your logs, and does not modify a
single file in your project or in the Isaac Lab install. It only reads and prints a table on your CLI.
