# You should always specify a full version here to ensure all of your developers
# are running the same version of Node.
FROM node:7.8.0

RUN apt-get update && apt-get install -y rsync

# Override the base log level (info).
ENV NPM_CONFIG_LOGLEVEL warn

# Install and configure `serve`.
RUN npm install -g serve
CMD serve -s build
EXPOSE 5000

WORKDIR /tmp
# Install all dependencies of the current project.
COPY package.json package.json
COPY npm-shrinkwrap.json npm-shrinkwrap.json
RUN npm install

WORKDIR /home/app/webapp
# Copy all local files into the image.
COPY . /home/app/webapp/
RUN rsync -K -a /tmp/node_modules /home/app/webapp/

# Build for production.
RUN npm run build --production
