# Midterm assignment
This is the complete midterm assignment. Each section will contain a link to all relevant files 
and/or repositories. 

## Project 1 - Testing Real Life Code
The code for the Testing Real Life Code can be found [here](../master/RecognitionAllIT.java)

The purpose of the original test is to expose the accuracy of the number plate recognition.
The only actual requirement for the test to pass is that it correctly reads the image and that 
it recognizes 53 out of 97 number plates.

The purpose of rewriting our test into what we have in [RecognitionAllIT](../master/RecognitionAllIT.java)
is to expose what images the program fails to recognize.

Parameterized tests in JUnit is a way to run a test one or multiple times given a certain dataset.
Say we have a set of data, like in this case, with 97 tuples we want to test, we really don't want to write
our test 97 times with different data. Instead we parse the data to the constructor of the
test class and we can then do a test with each tuple.
In this exercise I've used it by implementing a list with all the tuples which. When you 
execute one of the tests in the class, it will run through the list, and execute the test
once for every tuple.

Well, JUnit is a Java framework for unit testing, so it's definitely a JUnit test.
If we're discussing whether it was a unit test or an integration test, this was definitely
more an integration test than a unit test. The reason being, that we're actually also
testing that we are reading the files correctly. This happens in the constructor of
`CarSnapshot`.

Hamcrest matchers can be smart, since they provide you with the option to make your own matchers.
In this case, I didn't find it necessary to make my own matcher, so here it didn't really make
a difference. 

## Project 2 - Unit Testing, Testable Code, Mocking and Code Coverage
To make this code testable we implemented the pattern inversion of control by using
dependency injection. Further, we implemented a factory to have a way to get an instance
of the implementations of the `IJokeFetcher`. This gives us a lower coupling and a higher
cohesion as well.

The test results can be seen on the image below.
![Test results](../master/test-cases.png)




## Project 3 - Monopoly
The code for the Monopoly project can be found [here](https://github.com/ziemerz/monopoly)

In this project I have chosen not to follow the design of provided UML diagram. 
The reason for this is, that even though it reflects who takes what action in monopoly in 
a real life scenario, this way of doing it actually prevents a lot of polymorphism that you
can easily achieve by moving the responsibility of the classes. 

Here I'll walk you through how and why it was done the way it was. 

First of all, we chose to use Spring Boot instead of Spring IoC alone. Spring IoC requires
some manual configuration while Spring Boot is preconfigured. This makes it easier for us
to get started using the IoC container. 
Also, the documentation referenced from the assignment is completely outdated 
(we're at Spring 5.0.x now), and since 4.0.x it has been possible to do Java configuration
of beans instead of XML based. 

Anyway, we chose to give the `Game` interface the responsibility of handling the rules of the game.
That includes what happens when a player takes a turn. The `Player` type is then only a interface
with limited actions, and the rest is up to the `GameController` that do all the delegation of
tasks related to that game. 

The `Monopoly` class is an implementation of the `Game` interface, which makes it easy to
substitute for another type of game (ie. Matador), if we don't want to play Monopoly anymore.
This also makes it extremely easy to test, as all of our logic is now in the `Monopoly` class.

For the example, I've chosen to inject the mocks into the `MonopolyTests` using the `@MockBean`
annotation. This is usually only done in integration tests, where in unit tests, you would
usually inject the dependencies yourself, so you can manually reset them after each test to
clean state. Also, by using Spring, we start up a Spring container, which is completely
 unnecessary for doing unit testing.
 
In this case we're interested in testing the method `move` in the `Monopoly` class, since it
holds all the logic worth testing in this case. You could argue, that the method `move` in 
the `GameControllerImpl` class would be worth testing as well, as it limits what players
can do a move. 

We have chosen to only apply white-box testing in the form of unit testing in this case.
One could easily do black-box testing by doing boundary testing. Monopoly rules are widely
known, which is why we could easily do black-box testing.
The only boundaries on the board is the number of fields. There are 40 fields on a Monopoly
board. Here the lower boundary is 1 and the upper boundary is 40, and when we go above 40,
we want to start over again.
 