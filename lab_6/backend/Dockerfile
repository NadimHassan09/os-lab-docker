# Base image for Node.js runtime
# Using Node.js 20 which has all the tools I need to run my backend
# This image is based on Linux and comes with npm pre-installed
FROM node:20

# Set working directory inside container
# All the commands below will execute in this directory
# It's like the home directory for my application in the container
WORKDIR /app

# Copy package files and install dependencies
# Docker layer caching optimization: I copy package files first
# If I only change my code (not dependencies), Docker reuses the cached
# node_modules layer and doesn't reinstall packages - saves time!
# The package*.json pattern matches both package.json and package-lock.json
COPY package*.json ./
# Install all dependencies from package.json
# This creates the node_modules directory with all required packages
# Like express, mysql2, or whatever my backend needs
RUN npm install

# Copy application source code
# Now I copy all my backend code (server.js, routes, etc.)
# I do this after npm install so code changes don't invalidate the dependency cache
COPY . .

# Expose backend API port
# This is port 3000 where my Express server will listen
# EXPOSE is mostly documentation - the actual port mapping happens in docker-compose
# But it's good practice to document which ports the container uses
EXPOSE 3000

# Start the Node.js server
# CMD runs when the container starts
# I'm directly running server.js with node
# This is the entry point of my backend application
# The server.js file should start listening on port 3000
CMD ["node", "server.js"]