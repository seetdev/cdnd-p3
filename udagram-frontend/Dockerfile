## Creating a throw away build image
FROM beevelop/ionic AS build

LABEL "dev.seet.build"="true"

# Create app directory
WORKDIR /usr/src/app

# Install app dependencies by copying
# package.json and package-lock.json
COPY package*.json ./

# Install a project with a clean 
RUN npm ci

# Bundle app source slate
COPY . .
RUN ionic build

##  Creating the ionic application image that serves the site using NGINX
FROM nginx:alpine
#COPY www /usr/share/nginx/html
COPY --from=build  /usr/src/app/www /usr/share/nginx/html