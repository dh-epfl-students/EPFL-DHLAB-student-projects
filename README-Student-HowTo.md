# DHLAB student projects - Technical specifications

Information for EPFL students doing a MA/BA semester project or master project at the EPFL-DHLAB.

See also information in these [slides](https://github.com/dhlab-epfl-students/) (EPFL only).


- [GitHub repository](#your-github-repository)
- [How-to: Student projects](#how-to-student-projects)
- [Various memos and links](#various-memos-and-links)
- [Data and Code](#data-and-code)

## Your GitHub repository:

### Naming
Please name your repository as follows:

- use lower case;
- use hyphens to separate tokens;
- if related to a larger project, start with the name of this project, followed by the name of your project (e.g. `impresso-image-classification`);
- in case of doubt, ask your supervisors;

### Structure
You are free to structure your repository as you wish, but we advise to have:

- a `notebooks` folder, for your working notebook;
- a `lib` folder, in case you convert your notebook in scripts with a command line interface;
- a `report` fodler, where you put the PDF and latex sources of your report;
- a README, with the information specified below.


### What should be in your README
- **Basic information**
    - your name
    - the names of supervisors
    - the academic year
- **About**: include a brief introduction of your project.
- **Research summary**: include a brief summary of your approaches/implementations and an illlustration of your results.
- **Installation and Usage**
    - dependencies: platform, libraries (for Python include a `requirements.txt` file)
    - compilation (if necessary)
    - usage: how to run your code
- **License**    
    We encourage you to choose an open license (e.g. AGPL, GPL, LGPL or MIT).
    License files are already available in GH (add new file, start typing license, choices will appear).
    You can also add the following at the end of your README:       
   
	    
	    project_name - Jean Dupont    
	    Copyright (c) Year EPFL    
	    This program is licensed under the terms of the [license]. 
	    


## Working with a remote EPFL server

If necessary the DHLAB can grant you access to a machine on the IC cluster:

- ask your supervisor to gain access;
- login with gaspar credentials: ```ssh [gasparname]@iccluster0XX.iccluster.epfl.ch where 'XX' is the machine nb```     
- the node usually has 
	- 256GB of RAM, 
	- 2 GPUs
	- 200GB of disk space on `/`
	- 12TB of disk space under `scratch`
-  :exclamation: **important**: the machine is shared and given ths small size of `/`, do not store your data (i.e. the data you work with, intermediary results, models, various resources, etc.) in your `home` but under `scratch/students` where you can do your own folder. 


For people using Python on a cluster node: 

- create a **local** python environment (using conda or pipenv)
- to easily code locally and run things remotely, configure your IDE to save your code on the remote serveur as you code (e.g. with [PyCharm](https://www.jetbrains.com/help/pycharm/creating-a-remote-server-configuration.html).
     

**How to access a notebook on a remote server**

In order to access a jupyter notebook which runs on a remote server you need to configure the jupyter server-client setting accordingly. Have a look [here](https://jupyter-notebook.readthedocs.io/en/stable/public_server.html#running-a-notebook-server). 

- run `jupyter notebook --generate-config`, this will create a `.jupyter` folder in your home (hidden, use `ls -a`) 
- use `jupyter notebook password` to set a password. 
- edit the `jupyter_notebook_config.py` file in order to set the port where jupyter will broadcast. The following three lines are needed, all the rest can be commented:    

```
c = get_config()
c.NotebookApp.ip = '0.0.0.0'
c.NotebookApp.port = 8990 <= change this port, for ex. 8890, 8790, etc.
```

You can ignore SSL certificates.

If you run `jupyter notebook` the notebook will start and be accessible at http://iccluster0XX.iccluster.epfl.ch:8890 (you need to enter your password)

In order to leave it open while you are executing things, you can run the notebook in a screen.


**How to create another shell session and detach from is: use `screen`**     

Main commands:

- create a session: `screen -S name_of_the_session`  =>  you are in
- go out of a session: `Ctrl-A D` => session still running, you are out
- reconnect to a session: `screen -r name_of_the_session`
- kill a session: from within the session, `Ctrl-A K`
- in case you are reconnecting from inside (by mistake):  `screen -rd name_of_the_session`
- to list all active screens: `screen -ls`

Documentation:

- Tutorial: [https://linuxize.com/post/how-to-use-linux-screen/](https://linuxize.com/post/how-to-use-linux-screen/) 
- Full documentation: [https://linux.die.net/man/1/screen](https://linux.die.net/man/1/screen)
- Also available via `man screen`

Steps to work with a notebook in a screen:

- `cd [your repo]`
- `screen -S work` => you are in a screen named "work" where you will launch the notebook
- activate your env
- start the nb (`jupyter notebook`) 
- check the url `http://iccluster0XX.iccluster.epfl.ch:8890`
- if all ok then exit the screen (`Ctr-a d`). You can now work in the notebook, open and close your browser as you want, it will keep running. 


