FROM node:16
### Build
FROM beevelop/ionic:latest AS ionic
## Create app directory
WORKDIR /usr/src/app
## Install app dependencies
## A wildcard is used to ensure both package.json AND package-lock.json are copied
COPY package*.json ./
RUN npm ci --force
## Bundle app source
COPY . .
# Use Node.js 16 as base image
# Set legacy OpenSSL provider
ENV NODE_OPTIONS=--openssl-legacy-provider
RUN npm install -g @ionic/cli
RUN ionic build --prod
### Run 
FROM nginx:alpine
#COPY www /usr/share/nginx/html
COPY --from=ionic  /usr/src/app/www /usr/share/nginx/html