# gallery
Link to live website: https://cytlin-ip-1.onrender.com
Forked and cloned repo
Created a database on cluster on MongoDB
Replaced MongoDB URL with my database URL.

Created a web hook
Used NGROK to create a public URL for my localhost on port 8080
Used the http URL as the payload URL
Configured my pipeline to be triggered after every commit pushed.
Installed Node plugin and configured it.
Configured Gradle tool
Created a pipeline with Build, Test and Deploy.
For the agent directive run it on node
In 'Build' used Gradle to build, 'npm install' to install dependencies
Hosted project on Render.
In 'Render' I used 'node server' to start the server
Added 'MILESTONE 2' to index.js

Switched to test branch
First run 'npm install' to install dependencies on Test branch
Run ‘npm test’
Merged test branch to master branch
Resolved conflicts
On the pipeline script in 'Test' stage run 'npm test' and added a check to see if test run successfully.
If tests fail an email is sent out to me 
Edited index.js and added 'MILESTONE 3'

Created a slack channel and configured it with Jenkins
Added a post directive to send a slack message with build id and website URL after a successful deploy
Added 'MILESTONE 4' to index.js
