# Creating Components

## Part 2: Implementing MathSender Behavior


Edit the MathSender.cpp to implement the component behavior. Use a text editor to make the following edits to MathSender.cpp.


The handler DO_MATH_handler is called when the MathSender component receives a DO_MATH command. This handler overrides the corresponding pure virtual function in the auto-generated base class. Fill in the handler so that it looks like this:

```cpp
// In: MathSender.cpp
void MathSender ::
  DO_MATH_cmdHandler(
      const FwOpcodeType opCode,
      const U32 cmdSeq,
      F32 val1,
      MathOp op,
      F32 val2
  )
{
  this->tlmWrite_VAL1(val1);
  this->tlmWrite_OP(op);
  this->tlmWrite_VAL2(val2);
  this->log_ACTIVITY_LO_COMMAND_RECV(val1, op, val2);
  this->mathOpOut_out(0, val1, op, val2);
  this->cmdResponse_out(opCode, cmdSeq, Fw::CmdResponse::OK);
}
```
@TODO add description of what the code does. 

Check the build using:
# HERE

```shell
# In: MathSender
fprime-util build
```

The handler mathResultIn_handler is called when the MathReceiver component code returns a result by invoking the mathResultIn port. Again the handler overrides the corresponding pure virtual function in the auto-generated base class. Fill in the handler so that it looks like this:

```cpp
// In: MathSender.cpp
void MathSender ::
  mathResultIn_handler(
      const NATIVE_INT_TYPE portNum,
      F32 result
  )
{
    this->tlmWrite_RESULT(result);
    this->log_ACTIVITY_HI_RESULT(result);
}
```

The implementation code emits the result on the RESULT telemetry channel and as a RESULT event report.

Check the build using:

```shell
# In: MathSender
fprime-util build
```

## Summary 
In this section you created the MathComponent and implemented the component's behavior. 