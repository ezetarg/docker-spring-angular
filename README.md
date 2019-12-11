# docker-spring-angular

This is a project to test an angular app and a spring boot backend.

## Commands
To build and run: `docker-compose up -d`

To stop and remove created containers: `docker-compose down --remove-orphans`

It was tested using:
- Docker version 18.09.7
- docker-compose version 1.17.1

Both the frontend and the backend are built in a 2-stage process.
In addition, a nginx is configured in order to serve the content using only one url (backend is mounted in /api/).
