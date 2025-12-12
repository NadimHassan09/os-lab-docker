# Base image for Node.js runtime
# I'm using Node.js version 20 which is the LTS (Long Term Support) version
# This gives me npm and node commands in the container
FROM node:20

# Set working directory inside container
# This is like doing 'cd /app' - all commands will run from here
# If the directory doesn't exist, Docker creates it automatically
WORKDIR /app

# Copy package files and install dependencies
# I copy package.json and package-lock.json first (before source code)
# This is a Docker optimization trick: if dependencies don't change,
# Docker can use cached layers and skip reinstalling everything!
# The * means it matches both package.json and package-lock.json
COPY package*.json ./
# Install all the npm packages listed in package.json
# This creates node_modules folder with all dependencies
RUN npm install

# Copy application source code
# Now I copy everything else (all my React components, config files, etc.)
# I do this after npm install because source code changes more often
# So Docker can cache the npm install step
COPY . .

# Expose application port
# This tells Docker that this container will listen on port 5173
# It's like a documentation note - doesn't actually open the port
# The docker-compose.yml port mapping actually makes it accessible
EXPOSE 5173

# Environment variables for Vite development server
# Vite is the build tool I'm using for React
# Setting HOST to 0.0.0.0 is important! It means listen on all network interfaces
# Without this, the server only listens on localhost and won't be accessible
# from outside the container (like from my browser on the host machine)
ENV HOST=0.0.0.0
ENV PORT=5173
ENV VITE_HOST=0.0.0.0
ENV VITE_PORT=5173

# Start development server
# CMD is the command that runs when container starts
# I'm running the dev script from package.json
# The --host 0.0.0.0 flag makes sure Vite binds to all interfaces
# This took me a while to figure out - was getting connection refused errors!
CMD ["npm", "run", "dev", "--", "--host", "0.0.0.0"]