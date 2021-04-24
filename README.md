Milestone 1: index.html added

Created docker image and ran container with 
docker run -dit --name project -p 5000:80 -v "$PWD":/usr/local/apache2/htdocs/ httpd:2.4
