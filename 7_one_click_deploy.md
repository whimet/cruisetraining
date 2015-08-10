#We'll setup one click deploy in this course

## Setup deploy stage ##
  * Open Cruise admin page
    1. Open Cruise in browser: http://localhost:8153
    1. Click "Administration" tab
  * Edit petclinic pipeline
    1. Click pipeline "Petclinic"
    1. Click "Edit this pipeline"
  * Add deploy stage
    1. duplicate the ut stage config from `<stage> to </stage>`
    1. change the new stage name to "deploy"
    1. change the ant target to "deploy\_to\_production"
    1. add the config in stage tag
```
    <approval type="manual"/>
```
    1. Click "Save"
  * Trigger a new pipeline
    1. Click "Current Activity" page
    1. Click "Force Build" button on the right
    1. Wait pipeline to be finished
    1. Verify that the build stopped at deploy stage
  * One click deploy
    1. Click "Pipeline activity" on the top
    1. Click "approval" button to do deploy
