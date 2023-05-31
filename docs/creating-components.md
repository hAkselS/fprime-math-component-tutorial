# Creating Components

## Part 1: MathSender

Start by creating and navigating to the directory where the components will live. 

```shell 
# In: MathProject
mkdir Components
cd Components 
```

The MathSender is going to be an active component which will send receive parameters, send parameters, log events, and send telemetry. With this is mind, use the following command to create the MathSender component. 

```shell
# In: Components
fprime-util new --component 
```
This command will prompt you for some inputs. You should specify the follow so that the components matches the short description above. 

```
[INFO] Cookiecutter source: using builtin
component_name [MyComponent]: MathSender 
component_short_description [Example Component for F Prime FSW framework.]: Active component used for sending operations and operrands to the MathReceiver.
Component_namespace[Component]: MathModule
Select component_kind:
1 - active
2 - passive
3 - queued
Choose from 1, 2, 3 [1]: 1
Select enable_commands:
1 - yes
2 - no
Choose from 1, 2 [1]: 1
Select enable_telemetry:
1 - yes
2 - no
Choose from 1, 2 [1]: 1
Select enable_events:
1 - yes
2 - no
Choose from 1, 2 [1]: 1
Select enable_parameters:
1 - yes
2 - no
Choose from 1, 2 [1]: 1
[INFO] Found CMake file at 'MathProject/project.cmake'
Add component Components/MathSender to MathProject/project.cmake at end of file (yes/no)? yes
Generate implementation files (yes/no)? yes
```
Before doing anything to the files you have just generated, try building. 

```shell 
# In: Components
fprime-util build
```


