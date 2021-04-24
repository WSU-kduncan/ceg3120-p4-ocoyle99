Milestone 1: index.html added

Created docker image and ran container with 
docker run -dit --name project -p 5000:80 -v "$PWD":/usr/local/apache2/htdocs/ httpd:2.4

Milestone 2: created DockerHub account
added workflow using 

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
