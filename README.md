# Midterm assignment
This is the complete midterm assign. Each section will contain a link to all relevant files 
and/or repositories. 

## Project 1 - Testing Real Life Code
The purpose of the original test is to expose the accuracy of the number plate recognition.
The only actual requirement for the test to pass is that it correctly reads the image and that 
it recognizes 53 out of 97 number plates.

The purpose of rewriting our test into what we have in (**insert link to RecognitionAllIT.java here**)
is to expose what images the program fails to recognize.

Parameterized tests in JUnit is a way to run a test one or multiple times given a certain dataset.
Say we have a set of data, like in this case, with 97 tuples we want to test, we really don't want to write
our test 97 times with different data. Instead we parse the data to the constructor of the
test class and we can then do a test with each tuple.
In this exercise I've used it by implementing a list with all the tuples which. When you 
execute one of the tests in the class, it will run through the list, and execute the test
once for every tuple.




## Project 2 - Unit Testing, Testable Code, Mocking & Code Coverage


## Project 3 - Monopoly
In this project I have chosen not to follow the design of provided UML diagram. 
The reason for this is, that even though it reflects who takes what action in monopoly in 
a real life scenario, this way of doing it actually prevents a lot of polymorphy that you
can easily achieve by moving the responsibility of the classes. 

Here I'll walk you through how and why it was done the way it was.  