**SENG 438 - Software Testing, Reliability, and Quality**


**Lab. Report \#4 – Mutation Testing and Web app testing**


| Group \#:         |  4  |
| ----------------- | --- |
| Student Names:    |     |
| Alexander Sembrat |     |
| Andrew Howe       |     |
| Hajin Kim         |     |
| Jenna Vlaar       |     |




# 1 Introduction


The purpose of this lab is to explore mutation testing and GUI testing. By introducing mutation faults in a Java program and using a mutation testing tool to interpret scores, we will learn the fundamentals of mutation testing and utilizing new testing tools. Using Selenium, we will automate test cases to become familiar with GUI testing. We will learn the differences between automated and manual GUI testing through designing test cases and utilizing Selenium. Overall, the aim of this lab is to learn the fundamentals of mutation and GUI testing and how to utilize automotive tools during these processes.




# 2 Analysis of 10 Mutants of the Range class


1. public boolean intersects(Range range)<br />
replaced boolean return with true for intersects → SURVIVED<br />
This mutation happens because we only tested a TRUE outcome, to fix this we implemented a test that also tests a FALSE outcome for the test.


2. public boolean contains(double value)<br />
changed conditional boundary → SURVIVED<br />
This mutation survived because we did not closely test the boundaries so small changes would allow the mutant to survive.


3. public boolean intersects(double b0, double b1)<br />
removed conditional - replaced comparison check with false → SURVIVED<br />
This mutation was survived because we did not have the test return false all possible ways, adding tests were the lower bound is the problem, and a test where the upperbound is the problem fixes this.


4. public boolean intersects(double b0, double b1)<br />
negated double field lower → SURVIVED<br />
This mutant survives because in the function the comparison is b0 <= this.lower. If we negate this.lower, the comparison becomes b0 <= -this.lower, which is not correct and will give incorrect results when the range has a negative lower bound.


5. private static double max(double d1, double d2)<br />
replaced return of double value with -(x + 1) for org/jfree/data/Range::max → KILLED<br />
This mutant is killed by our test suite, while we do not directly test this function as it is private it is used in other functions we test, when the return value is incremented by then then negated it will no longer be the maximum expected by our tests and will be killed.


6. public double getUpperBound()<br />
Incremented (a++) double field upper → KILLED<br />
This was killed because when the test expects the correct value, however the mutant adds 1 so the mutant is killed.


7. public double getCentralValue()<br />
Substituted 2.0 with 1.0 → KILLED<br />
This mutant is killed by our suite because the function returns the central value and our tests cover this, when 2.0 is substituted with 1.0 the answer changes so the test fails and kills the mutant.


8. public boolean intersects(Range range)<br />
replaced return of integer sized value with (x == 0 ? 1 : 0) → KILLED<br />
This mutant is killed because our tests correctly identify if intersects is true or false and this mutant swaps the value so it fails the test and is killed.


9. public static Range combine(Range range1, Range range2)<br />
not equal to equal → KILLED<br />
Our test suite kills this mutant because if != is replaced with equal the Null range will continue through the function and therefore return the incorrect value that our tests will detect.


10. public boolean intersects(double b0, double b1)<br />
Negated double field lower → KILLED<br />
This mutant is killed by our suite becuase if the lower value of the range is negated, then the answer will change and our test will detect a failure. This is because our test originally had a very small discrepancy between the ranges so negating caused the opposite result in the if statement.


# 3 Report all of the statistics and the mutation score for each test class
Here are the statistics from before:


### Range Class
![](PIT Test Coverage Report Range.png)

### DataUtilities Class
![](PIT Test Coverage Report DataUtilities.png)



# 4 Analysis drawn on the effectiveness of each of the test classes


Statistics for After we added more tests:


### Range Class 
![](PIT Test Coverage Report Range After.png)

In lab 3 we misunderstood the instructions and thought we had to write tests for all of the remaining methods in the range class, therefore it was very difficult to raise the mutant test coverage by 10% as we already had a good number because of our extensive test suite from the last assignment. The mutants became very hard and sometimes impossible to kill, for example there are increment mutants we cannot kill because they increment after the return so they will be correct and we cannot kill them. If we take all of the extra tests we wrote last week and remove them we get a much greater increase.


### DataUtilities Class
![](PIT Test Coverage Report DataUtilities After.png)

Similarly to the range class there were additional methods added last week that we thought we had to write tests for so our original mutation coverage of 89% is very high, it was extremely difficult to raise the coverage even a few %, but because it's already so high we thought it was acceptable. Most of the remaining mutants cannot be killed.


# 5 A discussion on the effect of equivalent mutants on mutation score accuracy


Equivalent mutants are mutants which exhibit behavior identical to the program it has been created for. Equivalent mutants should not have an effect on mutation score


# 6 A discussion of what could have been done to improve the mutation score of the test suites
	
The way to improve the mutation score of the test suite is to find a way to kill any existing mutants in the system. Any tests that should have failed during the addition of mutants should be covered by new tests. By viewing the PITest report, we can see what mutants were introduced and thus draw conclusions on what we should test on. 


# 7 Why do we need mutation testing? Advantages and disadvantages of mutation testing


All types of testing aim to remove faults within a software and ensure the quality of a test suite. Mutation testing is useful in identifying unknown defects within a software. By introducing defects into a test suite, developers can determine if a test suite is able to detect these faults. In this way, mutation testing has the ability to detect a large number of 
defects within the code and ensure a system has high coverage and overall quality. Mutation testing is disadvantageous in that some mutations are difficult and/or time-consuming to implement. This means that the mutation testing process can become very expensive as well as nearly impossible without automation or comparing against the original test suite.


# 8 Explain your SELENIUM test case design process


SELENIUM test cases were designed to carry out a simple sequence of events that may produce errors in the website. We had to cover at least 8 different functionalities of the system, so we wanted to ensure the basic functionalities of an online shopping application were covered. We first drew basic requirements of the system. We decided these as follows: checking out, searching for items, viewing account information, logging in, logging out, viewing items, adding items to cart and viewing cart. Once these were decided, it was simple to produce individual tests that met one requirement each. 


# 9 Explain the use of assertions and checkpoints

Asserts ensure that the application is producing the exact behavior that is expected of the system. Requirements that are imperative to the system’s integrity will likely be coded using a hard assert which will abort the testing process if a certain requirement is not met. Alternatively, less important requirements in the system will simply give an error message but will allow the test case to complete. Assertions are used during testing to ensure the system is functioning correctly. Checkpoints are used to define the scope of assertions. They allow a system to be restored to a certain point in time in case of failure or to compare to a future state of the system. Checkpoints are useful in verifying that a system’s state has not been changed after the execution of a testing process. 


# 10 How did you test each functionality with different test data?


For each test case, we could test functionality by inputting different inputs into the ‘value’ field on Selenium. For example, we could input an incorrect username and password and the login test would fail. 


# 11 Discuss advantages of Selenium vs. Sikulix


Selenium and SikuliX are both simple automated test tools that anybody would be able to use. SikuliX is disadvantageous in that changing the original application will require you to rewrite tests while Selenium is more adaptive to system updates. Selenium is disadvantageous in that it cannot test image-based applications where SikuliX can. Selenium automatically implemented verification checkpoints while SikuliX did not. Both automation tools are not compatible with dynamic systems and would automatically fail tests if pop-ups or other changes to the system occurred. This is a large disadvantage on testing with these tools.


# 12 How the team work/effort was divided and managed


All of us worked together to download and install the needed tools and files onto our computers. Then, we divided the test cases that failed the JUnit tests between us to be corrected in order to begin our mutation testing. After we ran our mutation tests, we reviewed the results together and reported our findings. We again downloaded and installed the needed tools for GUI testing. We each selected 2 of the 8 requirements listed above and began using Selenium to create our tests. We again reported our results and compared the use of Sikulix to this process.




# 13 Difficulties encountered, challenges overcome and lessons learned


We had a lot of difficulty trying to get all of the test cases to pass in order to begin mutation testing. Eventually we passed all of the tests and were able to begin mutation testing. The automated processes were not challenging however it was difficult trying to decide how to increase the mutation score. We learned how to read the mutation summary and ended up increasing each mutation score for DataUtilities and Range classes.




# 14 Comments/feedback on the lab itself


There was not much guidance on how to use and operate the tools required of us during this lab. We had to do all of our learning and research on our own. We also had a lot of trouble downloading our files as the jar files were all very spread out and the assignment 4 artifacts did not contain one of the jar files necessary in order to run the tests. So it ended up taking several hours to simply set up our test suite properly. The lab report itself also contained about twice the amount of questions as the previous assignments so it took extra time to complete that as well. Overall, the lab was not too intensive but it would have been completed in a way more reasonable amount of time if the assignment files were organized properly or we had written explanations on how to set up our suite and use the assignment tools.
