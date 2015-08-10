#This workshop is targeted for demonstrating workflows, parallelization, pipeline dependencies features of Cruise.

## Preparation ##
  * We have configured the Petclinic pipeline in previous workshop, now change the Petclinic project to use the following Svn repository: http://localhost/svn/petclinic/branches/1.1
    * Open Cruise admin page
      1. Open Cruise in browser: http://localhost:8153
      1. Click "Administration" tab
    * Edit Petclinic pipeline
      1. Click pipeline "Petclinic"
      1. Click "Edit this pipeline"
    * Change material url
      1. Change `<svn url="http://localhost/svn/petclinic/branches/1.0"/> to <svn url="http://localhost/svn/petclinic/branches/1.1"/>`
      1. Click "Save"
  * Go to "Current Activity" page, take a look at the current build (Cruise will schedule a new build because the url has changed)

## Question ##
If the build takes too long, what can we do?

  * Staged build
  * Parallelization

## Setup multiple stages ##
  * Open Cruise admin page
    1. Open Cruise in browser: http://localhost:8153
    1. Click "Administration" tab
  * Edit Petclinic pipeline
    1. Click pipeline "Petclinic"
    1. Click "Edit this pipeline"
  * Change to two stages
    1. Duplicate the current stage config (`from <stage> to </stage>`)
    1. Change the first stage name to "ut", and target in ant to "ut"
    1. Change the second stage name to "ft", and target in ant to "ft"
    1. Click Save
  * Trigger a new pipeline
    1. Click "Current Activity" page
    1. Click "Force Build" button on the right
    1. Wait pipeline to be finished
    1. Verify that the first stage only run the ut target

## Setup distributed build ##
  * Now we have ut, ft\_mysql, and ft\_hsql in the repository: http://localhost/svn/petclinic/branches/1.1
  * Setup build grid
    1. find a pair, and get the ip address
    1. open command line
    1. type command: cd c:\workspace\agent
    1. type command: java -jar c:\workspace\ci\_tools\cruise\_installers\agent-bootstrapper.jar <IP address of your pair>
  * Open Cruise admin page
    1. Open Cruise in browser: http://localhost:8153
    1. Click "Administration" tab
  * Edit Petclinic pipeline
    1. Click pipeline "Petclinic"
    1. Click "Edit this pipeline"
  * Change the material to http://localhost/svn/petclinic/branches/1.1
  * Change to two job in ft
    1. Duplicate the current job config in ft
    1. Change the first job name to "ft\_hsql", and target in ant to "ft\_hsql"
    1. Change the second job name to "ft\_mysql", and target in ant to "ft\_mysql"
    1. Click Save
  * Trigger a new pipeline
    1. Click "Current Activity" page
    1. Click "Force Build" button on the right
    1. Wait pipeline to be finished
    1. Verify that the two job in ft stage runs in the same time
    1. Understand how can we decrease the build time by using the distributed build

## Run build on different environment ##
  * Add resource for agent
    1. Click "Agents" tab
    1. Click "Specify Resources" on the remote agent, and input "mysql"
    1. Click "Specify Resources" on the local agent, and input "hsql"
  * Add resource for job
    1. Click "Administrator" tab
    1. Click pipeline "Petclinic"
    1. Click "Edit this pipeline"
    1. Add resource settings under the ft\_mysql job tag
```
    <resources><resource>mysql</resource></resources>
```
    1. Add resource settings under the ft\_hsql job tag
```
    <resources><resource>hsql</resource></resources>
```
  * Trigger a new pipeline
    1. Click "Current Activity" page
    1. Click "Force Build" button on the right
    1. Wait pipeline to be finished
    1. Verify that the ft\_mysql job only runs on the remote agent and ft\_hsql only runs on local agent
    1. Understand how can we run the build on different environment

## Setup pipeline dependency ##
  * Setup a "dist" stage in pipeline "Petclinic"
    1. Click "Administration" tab
    1. Click "Edit this pipeline" to change the Svn repository to the following URL: http://localhost/svn/petclinic/trunk
    1. Add a new "dist" stage at the end of pipeline configuration use "performance" as the Ant target
    1. Add artifact definition:
```
	<artifacts><artifact src="target\dist\petclinic.war"/></artifacts>
```
    1. Submit your changes
    1. Go to the "Current Activity" page to trigger a new pipeline
  * Setup a new pipeline named "Petclinic\_performance\_testing"
    1. Click "Administration" tab
    1. Click "Add new pipeline"
    1. Specify pipeline name "Petclinic\_performance\_testing" and use the following Svn repository: http://localhost/svn/petclinic/trunk
    1. Click "Add this pipeline" to submit
    1. Change the Ant target to "performance" in job configuration
  * Change the new pipeline to depend on "Petclinic" pipeline
    1. Click "Administration" tab
    1. Click "Petclinic\_performance\_testing" on the left side
    1. Click "Edit this pipeline"
    1. Add the following xml inside the materials tag
```
    <pipeline pipelineName="Petclinic" stageName="defaultStage"/>
```
  * Fetch artifact from the "Petclinic" pipeline
    1. Add the following in jobs/job/tasks tag
```
    <fetchartifact pipeline="Petclinic" stage="dist" job="defaultJob" srcfile="petclinic.war"/>
```
    1. Click "Save"
  * Trigger a new pipeline for "Petclinic"
    1. Click "Current Activity"
    1. Click "Force Build" button on the right
    1. Wait pipeline to be finished
    1. Verify that the "Petclinic\_performance\_testing" pipeline will be triggered automatically