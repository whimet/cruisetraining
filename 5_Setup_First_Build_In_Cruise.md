#This workshop is targeted to a basic understanding about how build is running in Cruise.

## Prerequisite ##

  * Sample project with build script
  * Unit tests with reporting in sample project
  * Cruise server/agent environment

## Background ##

Now you have a simple project that contains sources and some unit tests. But you don't have automated build. In this workshop we will setup the project and make it running in Cruise.
## Introduction of the sample project ##
  * Petclinic is a web based application
  * We have the following three versions of the application
    1. 1.0 - contains scripts for compile and unit test
    1. 1.1 - contains functional test, it would take a long time to finish a full build
    1. trunk - contains performance test

## Steps for setting up the first build ##
  1. Open Cruise by double click "Cruise server" on Desktop
  1. Click Administration tab
  1. Click "Add new pipeline"
  1. Input pipeline name: Petclinic
  1. Input url: http://localhost/svn/petclinic/branches/1.0
  1. Input username: svnuser, password: svnpwd
  1. Click "Check connection" to test if svn connection works
  1. Click "Add this pipeline" to add the pipeline
  1. Cruise will forward you to the "Current Activity" page
  1. Watch the "Current Activity" page to see how your build is running

## Steps for getting junit report of your build ##
  * Change pipeline configuration to upload junit report as test artifact
    1. Click Administration tab
    1. Click "Edit this pipeline"
    1. Add the following setting inside job tag
```
 	<artifacts><test src="target\junit-reports"></test></artifacts>
```
  * View test result in job detail page
    1. Rerun your build and wait it to be finished
    1. We can know how many tests failed and how many tests passed, but no detail information
  * Add sub tab to show junit report detail
    1. Click Administration tab
    1. Click "Edit this pipeline"
    1. Add the following setting inside job tag
```
    <tabs>
      <tab name="JUnit-Reports" path="junit-reports/html/index.html" />
    </tabs>
```
  * View Result in Dashboard
    1. Click "Current Activity" on the top
    1. Click the "defaultJob" in Petclinic pipeline to go to the "Job Detail" page
    1. Verify there's a new tab named "JUnit-Reports"
    1. Click "JUnit-Reports"
    1. Verify that you can view the junit reports here

## Steps for getting artifacts from the build ##
  * Change pipeline configuration to upload war file
    1. Click Administration tab
    1. Click "Edit this pipeline"
    1. Add the following setting inside job tag
```
 	<artifacts><artifact src="target\dist"></file></artifacts>
```
  * View artifact in job detail page
    1. Rerun your build and wait it to be finished
    1. Click the "defaultJob" in Petclinic pipeline to go to the "Job Detail" page
    1. Click "Artifacts"
    1. Verify that you can download the petclinic.war from the dist folder