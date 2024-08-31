

     Hello!

     I created this script and module to avoid using GitHub Actions workflow,

     For building Static site output using NodeJS frameworks,

     and then deploy the output into gh-pages.

      but I see It could easily be used for PHP, Go,

      it does not acount for complex combined SSR/CRS environments, but everything is possible

      this can definitelly be further enhanced to make it booth

       push & pull on multiple remotes simulateously    

      I does ask for $SourcePath here you can specify that your environment does output into FOOBAR

     This script automates the process of building and deploying a web application

     from a source repository to a destination folder. It is designed to be used as part of a CI/CD pipeline.

     ---------------------------------------------------------------------------------------------

---------------------------------------------------------------------------------------------

     >> !!!!!! Prerequirities !!!!

    *     Git installed on your system.

    *    Node.js and npm installed for building the application

     This script will ask you for a few variables now.

     1) SourceRepoBranch : Path to the source repository branch (default: main)(e.g., main or master, foo)

     2) SourceRepoRoot : Path to the root of the source repository

3) SourcePath : Path to the built files in the source repository

4) destinationPath : Path to the destination folder

5) DeploymentBranch : Deployment branch (e.g., gh-pages or master)

6) MainshortDescription : Commit message for the main branch (has prefix of time and date)

7) DeploymentshortDescription : Commit message for the deployment branch (has prefix of time and date)

8) longDescription : Long description: What has changed outside of the building processes (has prefix of build process description)

"

)