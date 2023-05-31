# Creating Components

## Part 4: Implementing MathReceiver Behavior


Fill in the mathOpIn handler: In MathReceiver.cpp, complete the implementation of mathOpIn_handler so that it looks like this:

```cpp
void MathReceiver ::
  mathOpIn_handler(
      const NATIVE_INT_TYPE portNum,
      F32 val1,
      const MathOp& op,
      F32 val2
  )
{

    // Get the initial result
    F32 res = 0.0;
    switch (op.e) {
        case MathOp::ADD:
            res = val1 + val2;
            break;
        case MathOp::SUB:
            res = val1 - val2;
            break;
        case MathOp::MUL:
            res = val1 * val2;
            break;
        case MathOp::DIV:
            res = val1 / val2;
            break;
        default:
            FW_ASSERT(0, op.e);
            break;
    }

    // Get the factor value
    Fw::ParamValid valid;
    F32 factor = paramGet_FACTOR(valid);
    FW_ASSERT(
        valid.e == Fw::ParamValid::VALID || valid.e == Fw::ParamValid::DEFAULT,
        valid.e
    );

    // Multiply result by factor
    res *= factor;

    // Emit telemetry and events
    this->log_ACTIVITY_HI_OPERATION_PERFORMED(op);
    this->tlmWrite_OPERATION(op);

    // Emit result
    this->mathResultOut_out(0, res);

}
```

This code does the following:

    1. Compute an initial result based on the input values and the requested operation.

   2. Get the value of the factor parameter. Check that the value is a valid value from the parameter database or a default parameter value.

   3. Multiply the initial result by the factor to generate the final result.

   4. Emit telemetry and events.

   5. Emit the result.

Note that in step 1, op is an enum (a C++ class type), and op.e is the corresponding numeric value (an integer type). Note also that in the default case we deliberately fail an assertion. This is a standard pattern for exhaustive case checking. We should never hit the assertion. If we do, then a bug has occurred: we missed a case.

