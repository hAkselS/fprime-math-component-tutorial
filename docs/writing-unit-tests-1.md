# Writing Unit Tests

## Part 1: setting up the test

In Components/MathSender, create a directory called UnitTests 

```shell 
# In: MathSender
mkdir -p UnitTests
```

Add the unit test to the build. Absolutely make sure that this is BELOW the existing stuff in the CMakeLists.txt:

```cmake 
# In: MathSender/CMakeLists.txt
# Below: register_fprime_module()

set(UT_SOURCE_FILES
  "${CMAKE_CURRENT_LIST_DIR}/MathSender.fpp"
)
set(UT_AUTO_HELPERS ON)
register_fprime_ut()
```

Generate and implement the unit tests: 

```shell 
# In: MathSender
fprime-util generate --ut 
fprime-util impl --ut
```
    These may take a while

You haved just generate three new files ```Tester.cpp Tester.hpp TestMain.cpp```. Move these files to the UnitTests directory in MathSender using:

```shell 
# In: MathSender
mv Tester.* TestMain.cpp UnitTests
```

Now you need to add ```Tester.cpp and TestMain.cpp``` to the build. Do so by editing the CMakeLists.txt in MathSender: 

```cmake
# In: MathSender/CMakeLists.txt 
set(UT_SOURCE_FILES
  "${CMAKE_CURRENT_LIST_DIR}/MathSender.fpp"
  "${CMAKE_CURRENT_LIST_DIR}/UnitTests/Tester.cpp"
  "${CMAKE_CURRENT_LIST_DIR}/UnitTests/TestMain.cpp"
)
set(UT_AUTO_HELPERS ON)
register_fprime_ut()
```

    Note: most of this is from a few steps ago, you will only be adding two lines in this step. 

Build the unit test in MathSender:

```shell 
# In: MathSender
fprime-util build --ut 
```
    Don't forget the --ut or else you are just going to build the component again. 

    