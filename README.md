# Docker-Implementation

Docker Registry Browser

#Build Status: COMPLETE as of 12/12/19

#Author:Rishav Giri

Web Interface for the Docker Registry HTTP API V2 written in Ruby on Rails.

Usage
Docker
Execute:

docker run --name registry-browser -it -p 8080:8080 -e DOCKER_REGISTRY_URL=http://your-registry:5000 klausmeyer/docker-registry-browser
Manual setup
Install ruby e.g. using RVM
(see .ruby-version file for required version).
Execute the following command inside your local clone of this repository:
gem install bundler && bundle install --without development test
Run the application using
DOCKER_REGISTRY_URL=http://your-registry:5000 bundle exec bundle exec puma -C config/puma.rb
Configuration
The configuration is done by environment variables.

Option	Required	Type	Description
DOCKER_REGISTRY_URL	yes	String	URL to the Docker Registry which should be browsed
Example: http://your-registry:5000
NO_SSL_VERIFICATION	no	Bool	Enable to skip SSL verification (default false)
Example: true
BASIC_AUTH_USER	no	String	Username for basic-auth against registry
Example: joe
BASIC_AUTH_PASSWORD	no	String	Password for basic-auth against registry
Example: supersecretpassw0rd
TOKEN_AUTH_USER	no	String	Username for token-auth against registry
Example: joe
TOKEN_AUTH_PASSWORD	no	String	Password for token-auth against registry
Example: supersecretpassw0rd
ENABLE_DELETE_IMAGES	no	Bool	Allow deletion of tags (default false)
Example: true
PUBLIC_REGISTRY_URL	no	String	The public URL to the Docker Registry to do docker pull
Example: your-registry:5000
You can also set the following variables as Docker Swarm secrets with the same naming:

BASIC_AUTH_USER
BASIC_AUTH_PASSWORD
TOKEN_AUTH_USER
TOKEN_AUTH_PASSWORD
Proxy Setups
If you're using a reverse-proxy setup with SSL termination in front of this application in combination with ENABLE_DELETE_IMAGES=true you must make sure that the application knows about this fact (by sending X-Forwarded-Proto: https in the HTTP headers).

Otherwise the application would throw errors like "HTTP Origin header [...] didn't match request.base_url [...]" when you're trying to delete image-tags.
