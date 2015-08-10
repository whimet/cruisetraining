#Preparation for CI

# Introduction #

We will introduce the three basic components in CI:
  * Version Control System
  * Automated build
  * Automated test

## Version Control - Question ##
Have you used version control system before?
> if yes, which one have you used?
> > Do you have any pain point about it?

## Introduction of DVCS and CVCS ##

## Workshop for svn ##

  * Setup svn repository
    1. double click "VisualSVN-Server-2.0.7.msi" to install svn server, click "Next" for the following steps until "Custom Setup", deselect the "Use secure connections(https://)" option, and use default setting for the rest
    1. after finished, open VisualSVN Server management window
    1. click "Create new user..."
    1. input username "svnuser" and password "svnpwd"
    1. click "Create new repository"
    1. input repository name "test"
    1. check "Create default structure" and click OK
    1. check the default structure of the repository which include trunk, branches and tags

  * Install TortoiseSVN
    1. double click "TortoiseSVN-1.6.5.16974-win32-svn-1.6.5.msi", click next for each step (Restarting machine is optional here)

  * Put a new project into svn
    1. open Explorer
    1. right click on d:\workspace, and select "SVN Checkout..."
    1. input URL: https://localhost/svn/test/trunk, click ok to check out the project
    1. open test folder, right click, select New -> Text Document, change the filename to test.txt
    1. right click in test folder, select "SVN Commit..."
    1. double check the changes in the popup, and select the file "test.txt"
    1. input commit message "add new file test.txt"
    1. click ok to commit

  * Edit existing file
    1. Right click on the project folder
    1. select "SVN Update"
    1. double click file "test.txt", and input something
    1. right click in test folder, select "SVN Commit..."
    1. double check the changes in the popup, you can double click the changed item to view your changes
    1. input commit message "add new file test.txt"
    1. click ok to commit


## introduce test ##
Write test is to make sure the functionality works now and in future. Because the test would fail if the code doesn't work, so you don't afraid that your changes to one component would break other existing code.

what we are testing
  * unit test
  * integration test
  * function test


## Workshop for junit test ##
  * what we'll learn
    1. understand the execution order when run junit test
    1. write a simple unit test

  * understand the execution order when run junit test
    1. open the project 3\_junit\_workshop in eclipse
    1. open file test/util/MathTest.java
    1. click run to run MathTest
    1. we can know the execute order from the console output

  * write a simple unit test
    1. add the following code into MathTest.testAdd method
> > > Math math = new Math();
> > > assertThat(math.add(1, 2), Is.is(3));
    1. click run to run the MathTest
    1. check the result in JUnit tab in eclipse
    1. now change the Math.add method with the following code:
> > > return first + second;
    1. click run to run the MathTest again
    1. verify the test result is passed


## Workshop for ant ##
  * what we'll learn
    1. compile java project using ant
    1. run junit test using ant
    1. manage target dependency in ant
    1. generate junit report using ant

  * compile java project using ant
    1. copy file content from 1\_build-initial.xml to build.xml
    1. run "ant" on command line
    1. view the build file, check build target to understand how java compile works

  * run junit test using ant
    1. copy file content from 2\_build-test.xml to build.xml
    1. run "ant build test" on command line
    1. check the new added junit part in build file

  * manage target dependency in ant
    1. copy file content from 3\_build-dependency.xml to build.xml
    1. run ant on command line
    1. check the added dependency part

  * generate junit report using ant
    1. copy file content from 4\_build-report.xml to build.xml
    1. run ant on command line
    1. check the added junit-report part