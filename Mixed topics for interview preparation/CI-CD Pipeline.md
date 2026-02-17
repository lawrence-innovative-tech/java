#### **Purpose
- **CI (Continue Integration) -** Automate repeated work Build, test, scan to process pipeline.
- **CD (Continue Deployment) -** After CI completes followed by deployment.
- There are many ways to create ci/cd pipeline.
	1. GitHub actions
	2. Jenkins
	3. GitLab
- Ci-CD pipeline is event driven design, when code push repository ci/cd pipeline get triggers, run unit and integration test, if test has failed reports to particular developer.
- Success testing take build and deploy to staging to test application.
#### **Top companies code maintenance
-  There are three type of maintenance
	1. Current or Working branch
	2. Release Branch
	3. Production Setup (Master or Main)
1. Current or Working branch - Clone master code or setup to new branch, once complete our code runs push into GitHub it's started ci(test, build, create PR to if testing exist).
2. Release Branch - Once passes all the testing code moves to Release branch to production deployment.
3. Production branch - After deployment monitors few days on production. Then merge to master or main.