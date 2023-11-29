# Testing in General

## Tips

For any test of any language, the result should be preferred to be tested as opposed to the implementation. For example, if testing a function that adds two numbers, assume the body of the function is unknown, and test the result of running the function with various inputs.

This cannot be done in all cases. E.g:

- Testing Rust in the browser with no way to compile/run the code
- The code does not run, because it is incomplete or contains syntax errors
