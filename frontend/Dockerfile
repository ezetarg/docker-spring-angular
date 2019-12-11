### STAGE 1: Build ###
FROM node:10 as builder

WORKDIR /ng-app
RUN git clone https://github.com/ezetarg/angular-sample3.git .

WORKDIR /ng-app-temp
## Storing node modules on a separate layer will prevent unnecessary npm installs at each build
RUN cp /ng-app/package.json . && cp /ng-app/package-lock.json . && npm i && mv ./node_modules /ng-app/

WORKDIR /ng-app
## Build the angular app in production mode and store the artifacts in dist folder
RUN $(npm bin)/ng build --prod --output-path=dist

### STAGE 2: Setup ###
FROM nginx:stable-alpine

COPY ./nginx.conf /etc/nginx/conf.d/default.conf

## Remove default nginx website
RUN rm -rf /usr/share/nginx/html/*

## From ‘builder’ stage copy over the artifacts in dist folder to default nginx public folder
COPY --from=builder /ng-app/dist /usr/share/nginx/html

CMD ["nginx", "-g", "daemon off;"]
