#How to install Ant on Windows.

# Prerequisite #

  * Make sure you have JDK installed
  * Make sure %JDK\_Home%\bin in your system path (otherwise ant will complain can not finding tools.jar)

# Details #
  * Unzip apache-ant-1.7.1-bin.zip to C:\Program Files
  * Edit environment variable 'Path' to append the Ant bin directory: C:\Program Files\apache-ant-1.7.1\bin
  * Launch a new command window and run "ant -version" to verify it