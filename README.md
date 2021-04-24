    Create README.md in main folder of your repo that details the following:
        Project Overview
        Run Project Locally
            how you installed docker + dependencies (WSL2, for example)
            how to build the container
            how to run the container
            how to view the project (open a browser...go to ip and port...)
        Configure AWS CLI
            need AWS IAM user with admin credentials
            how you installed
            how to configure
        Create ECR
            command to create
        Configure GitHub Secrets
            need AWS IAM user with admin credentials
            set secrets and secret names
        Configure GitHub Workflow
            variables to change (AWS_REGION, etc.)

Documentation requirements using DockerHub

    Create README.md in main folder of your repo that details the following:
        Project Overview
        Run Project Locally
            how you installed docker + dependencies (WSL2, for example)
            how to build the container
            how to run the container
            how to view the project (open a browser...go to ip and port...)
        Configure AWS CLI
            need AWS IAM user with admin credentials
            how you installed
            how to configure
        Create DockerHub public repo
            process to create
        Configure GitHub Secrets
            what credentials are needed - DockerHub credentials (do not state your credentials)
            set secrets and secret names
        Configure GitHub Workflow
            variables to change (repository, etc.)



> 1.) Run Project Locally
In order to run the project locally, I first had to install docker. I already has WSL installed.

Next I built the container by running the command "docker build -t [name]:[tag]"

In order to run the container you must run the command "docker run -d -p 80:80 [name]:[tag]"

Once you have accomplished this you can test your work by running over to your favorite web browser and searching 127.0.0.1:80 and attempting a connection with your apache2 server!

> 2.) Create DockerHub repo
Unfortunately I was incapable of making the ECR on AWS because by the time I started this project the service had been removed for us. So I made a DockerHub account by following the steps in the project. I made my repo public and named it "project4".

Once I had made my account I went back to GitHub and added my workflow as instructed with the following code.

```name: Publish Docker image
on:
  release:
    types: [published]
jobs:
  push_to_registry:
    name: Push Docker image to Docker Hub
    runs-on: ubuntu-latest
    steps:
      - name: Check out the repo
        uses: actions/checkout@v2
      - name: Push to Docker Hub
        uses: docker/build-push-action@v1
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}
          repository: ocoyle99/project4
          tag_with_ref: true
```

> 3.) Create GitHub Secrets
Afterwards I went to add secrets to my GitHub repo and added the values for `DOCKER_USERNAME` and `DOCKER_PASSWORD`.
