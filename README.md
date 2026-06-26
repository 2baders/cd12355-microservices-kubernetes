This app is an analytics api that provides business analysts with usage data from space service, with daily check in and user visit report. 

It is containerized using docker, deployed on AWS EKS, with a postgresql db via helm on the cluster, using a t3-medium instance that gives enough resources to run comfortably without overkill.

Codebuild pulls the sourcecode from the repo, builds the image using the dockerfile, then pushes it tagged to AWS ECR.

Application is then deployed to the EKS cluster using kubernetes config files, that is a deployment.yaml that references the ecr image, a configmap for env variables, and a secret for encoded db password.

the eks cluster needs to have a nodegroup with 2 nodes minimum, one for the db and for the analytics-api. these two nodes will host the two pods. the DB is initally empty, but seeding files need to be ran through portforwarding. 

once db is seeded, apply the configmap, secret, and deployment yaml files to deploy the analytics-api to the cluster. 

for releasing new builds:
-update the repo
-run CodeBuild after editting the new imagetag
-replace the URI and imagetag in deployment.yaml to the new one.
-kubectl -f apply deployment.yaml

Thanks for viewing my project, please reply with feedback - Bader Alotaibi