# apptainer_build_example
Example how to to store apptainer on Dockerhub using github workflows in the Github packages.

Workflow on how to build the container can be found in .github/workflows/

## Set up DockerHub
1. Create an account at Dockerhub
2. Create a repostiroy on DockerHub
3. Create a personal access token for your Dockerhub to be able to push containers there (via account settings -> Personal access token -> gnerate new token -> set the token to write & read -> copy the token)

## Set up the Link between Dockerhub and Github
1. Go to your Github repository
2. Go to the settings of your project
3. Add a secret to your project (settings -> Secrets and variables -> Actions -> new repository secret): name the secret DOCKERHUB_TOKEN and paste your personal access token from DockerHub there in secrets

## Adapt the Github workflow yaml to your onw project
1. Change when you want to build the container
2. Change name of your apptainer definition file (line 28) to the name of the file in your project
3. Set the login name to your Dockerhub account name (line 34): echo ${{ secrets.DOCKERHUB_TOKEN }} | apptainer registry login -u [your_dockerhub_accountname] --password-stdin oras://docker.io
4. Set the link to the dockerhub repository: apptainer push container.sif oras://docker.io/[your_dockerhub_accountname]/[your_dockerhub_repository]:${tag}
