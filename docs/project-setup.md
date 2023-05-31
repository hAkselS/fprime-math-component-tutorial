# Project Setup 

## Bootstrapping F' 

An F´ project ties to a specific version of tools to work with F´. In order to create this project and install the correct version of tools, an initial bootstrap version of F´ tools must be installed. This is accomplished with the following command:

```shell
pip install fprime-tools
```

## Creating a New F' Project 

Now that the tools are installed, you can create the project where the math components will reside. 

To make a new project, run the following command and answer the questions as indicated below:

```shell
fprime-util new --project 
```
This command will require you to answer some questions. Answer as indicated below:

```
project_name [MyProject]: MathProject
fprime_branch_or_tag [devel]: devel
Select install_venv:
1 - yes
2 - no
Choose from 1, 2 [1]: 1
```

To start working on the new project two things need to happen. First you need to enter your project directory. Second, you need to start the python virtual environment that was created with your project. Use the two commands below to accomploish both these tasks.

```shell 
cd MathProject
. venv/bin/activate
```

You can check to make sure your virtual enviroment is working by looking at your command line. If youre virtual environment is running, you should see "(venv)" at the start of the your command line as below. 

```shell
(venv) MyName-MPB:fprime-math-component-tutorial myname$ 
```

## Summary 

In this seciton you have downnloaded F' tool which enable F' development. You created a new F' project which you develop further in this tutorial. You started running a virtual enviroment, which should be running whenever you are workong on this project.