# Defining Types 

## Starting Off 

In the context of the math component tutorial, types define the mathmatic operations that can be performed on the opperands.

To create the types, first create a directory where the types will reside and navigate into said directory. 

```shell
# In: MathProject 
mkdir -p MyTypes 
cd MyTypes
``` 

The types are defined in an fpp (F prime prime) file that you will create using the following command.

```shell 
# In: MyTypes
touch MathTypes.fpp
```

## Implementing to the Types 

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

To make sure MyTypes will build with the rest of the project, we need to create a CMakeLists.txt file and add MyTypes to project.cmake. 

## Adding to the Build 

To create CMakeLists.txt use:

```shell 
# In: MyTypes
touch CMakeLists.txt 
```

Note: capitalization is important! Use a text editor and replace whatever is in CMakeLists.txt the following.

```cmake 
set(SOURCE_FILES
  "${CMAKE_CURRENT_LIST_DIR}/MathTypes.fpp"
)

register_fprime_module()
```

Edit "project.cmake", which is in /MathProject and make sure to add the following lines. 

```cmake 
# Add in the types 
add_fprime_subdirectory("${CMAKE_CURRENT_LIST_DIR}/MyTypes/")
```

MyTypes directory should now build without any issues. Test the build with the following commmand before moving forward.

```shell 
# In: MyTyoes 
fprime-util build 
```

## Summary 
In the section of the tutorial you have created the MyTypes directory, MyTypes.fpp, defined four types, created a module, and added MyTypes to the build. 