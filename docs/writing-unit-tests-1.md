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
    Don't forget to add ```--ut``` or else you are just going to build the component again. 

Add a generic helper function so you can reuse code while writing unit tests. In Tester.cpp add the following:

```cpp
// In: Tester.cpp

void Tester ::
  testDoMath(MathOp op)
  {
    // Pick values
    const F32 val1 = 2.0;
    const F32 val2 = 3.0;
    // Send the command
    // pick a command sequence number
    const U32 cmdSeq = 10;
    // send DO_MATH command
    this->sendCmd_DO_MATH(0, cmdSeq, val1, op, val2);
    // retrieve the message from the message queue and dispatch the command to the handler
    this->component.doDispatch();
    // Verify command receipt and response
    // verify command response was sent
    ASSERT_CMD_RESPONSE_SIZE(1);
    // verify the command response was correct as expected
    ASSERT_CMD_RESPONSE(0, MathSenderComponentBase::OPCODE_DO_MATH, cmdSeq, Fw::CmdResponse::OK);
    // Verify operation request on mathOpOut
    // verify that one output port was invoked overall
    ASSERT_FROM_PORT_HISTORY_SIZE(1);
    // verify that the math operation port was invoked once
    ASSERT_from_mathOpOut_SIZE(1);
    // verify the arguments of the operation port
    ASSERT_from_mathOpOut(0, val1, op, val2);
    // Verify telemetry
    // verify that 3 channels were written
    ASSERT_TLM_SIZE(3);
    // verify that the desired telemetry values were sent once
    ASSERT_TLM_VAL1_SIZE(1);
    ASSERT_TLM_VAL2_SIZE(1);
    ASSERT_TLM_OP_SIZE(1);
    // verify that the correct telemetry values were sent
    ASSERT_TLM_VAL1(0, val1);
    ASSERT_TLM_VAL2(0, val2);
    ASSERT_TLM_OP(0, op);
    // Verify event reports
    // verify that one event was sent
    ASSERT_EVENTS_SIZE(1);
    // verify the expected event was sent once
    ASSERT_EVENTS_COMMAND_RECV_SIZE(1);
    // verify the correct event arguments were sent
    ASSERT_EVENTS_COMMAND_RECV(0, val1, op, val2);
  }
  ```
  
  Additionally, you should add the function signature in Tester.hpp:

  ```cpp 
// In: Tester.hpp
void testDoMath(MathOp, op); 
```

Write the acutal tester function using the helper funtion you just wrote:

```cpp 
// In: Tester.cpp 
void Tester ::
    testAddCommand()
  {
      this->testDoMath(MathOp::ADD);
  }
```

Add the function signature to Tester.hpp

```cpp
// In: Tester.hpp
void TestAddCommand(); 
``` 

Write a Google test macro in TestMain.cpp and make sure the test macro goes before main:

```cpp 
TEST(Nominal, AddCommand) {
    MathModule::Tester tester;
    tester.testAddCommand();
}
```

Run the test you have written. Make sure to execute the following in ```MathSender```. 

```shell 
# In: MathSender
fprime-util check 
``` 

