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

    This line tells the build system to make the unit test build depend on the STest build module.

   3. Add #include ```STest/Random/Random.hpp``` to ```TestMain.cpp```.

   4. Add the following line to the main function of ```TestMain.cpp```, just before the return statement:

```cpp
STest::Random::seed();
```

Recompile and rerun the tests. Now go to MathProject/build-fprime-automatic-native-ut/Components/MathSender and inspect the file ```seed-history```. This file is a log of random seed values. Each line represents the seed used in the corresponding run.

Sometimes you may want to run a test with a particular seed value, e.g., for replay debugging. To do this, put the seed value into a file ```seed``` in the same directory as ```seed-history```. If the file seed exists, then STest will use the seed it contains instead of generating a new seed.

Try the following:

   1. Copy the last value S of ```seed-history``` into ```seed```.

   2. In Components/MathSender, re-run the unit tests a few times.

   3. Inspect ```MathProject/build-fprime-automatic-native-ut/Components/MathSender/seed-history```. You should see that the value S was used in the runs you just did (corresponding to the last few entries in seed-history).

