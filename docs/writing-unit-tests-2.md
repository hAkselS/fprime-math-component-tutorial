# Writing Unit Tests 

## Part 2: Random testing

F Prime provides a module called STest that provides helper classes and functions for writing unit tests. As an exercise, use the interface provided by STest/STest/Pick.hpp to pick random values to use in the tests instead of using hard-coded values such as 2.0, 3.0, and 10.

Modifying the code: You will need to do the following:

   1. Add #include ```STest/Pick/Pick.hpp``` to Tester.cpp.

   2. Add the following line to ```Components/MathSender/CMakeLists.txt```, before ```register_fprime_ut```:

   ```cmake 
   # In: /MathSender/CMakeLists.txt
   set(UT_MOD_DEPS STest)
   ```

