## Creating a throw away build image
FROM node:12 AS build

LABEL "dev.seet.build"="true"

# Create app directory
WORKDIR /usr/src/app

# Install app dependencies by copying
# package.json and package-lock.json
COPY package*.json ./

# Install a project with a clean distribution
RUN npm ci --loglevel=error

# Bundle app source slate
COPY . .

# Transpiling the Typescript source
RUN npm run tsc

# Install a project with a clean distribution
RUN npm ci --production --loglevel=error

##  Creating the feed service image
FROM node:12

# Create app directory
WORKDIR /usr/src/app/

# Install app dependencies by copying
# package.json and package-lock.json
COPY --from=build /usr/src/app/package*.json /usr/src/app/
COPY --from=build /usr/src/app/www /usr/src/app/www
COPY --from=build /usr/src/app/node_modules /usr/src/app/node_modules

# Bind the port that the image will run on
EXPOSE 8080

# Define the Docker image's behavior at runtime
CMD ["node", "www/server.js"]