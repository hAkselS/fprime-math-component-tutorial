# Defining Types 

## Setup

In the context of the math component tutorial, types define the mathmatic operations that can be performed on the opperands.

To create the types, first create a directory where the types will reside and navigate into said directory. 

```shell
# In: MathProject 
mkdir -p Types 
cd Types
``` 

Types are defined in an fpp (F prime prime) file that you will create using the following command.

```shell 
# In: Types
touch MathTypes.fpp
```
Here you have created an empty fpp file named MathTypes in the Types directory.

## Implementing the Types 

Use your favorite text editor, visual studios, nano, vim, etc..., and add the following to MathTypes.fpp.

```
module MathModule{ 

    @ Math operations
    enum MathOp {
        ADD @< Addition
        SUB @< Subtraction
        MUL @< Multiplication
        DIV @< Division
  }
}
```
Above we have created an enumation of the four math types that we plan to use in this tutorial. Important note: think of the module similar to a cpp namespace. This module will be used in many files across the math comonent tutorial.

## Adding to the Build 

To make sure Types will build with the rest of the project, we need to create a CMakeLists.txt file and add Types to project.cmake. 

To create CMakeLists.txt use:

```shell 
# In: Types
touch CMakeLists.txt 
```

Note: capitalization is important! Use a text editor and replace whatever is in CMakeLists.txt, most likely nothing, with the following.

```cmake 
set(SOURCE_FILES
  "${CMAKE_CURRENT_LIST_DIR}/MathTypes.fpp"
)

register_fprime_module()
```

Edit "project.cmake", located in /MathProject, and make sure to add the following lines. 

```cmake 
# Add in the types 
add_fprime_subdirectory("${CMAKE_CURRENT_LIST_DIR}/Types/")
```

Types directory should now build without any issues. Test the build with the following commmand before moving forward.

```shell 
# In: Types 
fprime-util build 
```

## Summary 
In the section of the tutorial you have created the Types directory, Types.fpp, defined four types, created a module, and added Types to the build. 