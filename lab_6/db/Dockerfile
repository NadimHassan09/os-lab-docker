# Base image for MySQL database
# Using MySQL 8.0 which is a stable and widely used version
# This image comes with MySQL server pre-configured and ready to run
FROM mysql:8.0

# Copy initialization script to entrypoint directory
# This is a special directory that MySQL Docker image watches
# Any .sql files here get executed automatically when the database
# is first initialized (only on first run, not every restart!)
# Super useful for creating tables, inserting initial data, etc.
# My init.sql probably has CREATE TABLE statements
COPY init.sql /docker-entrypoint-initdb.d/

# MySQL environment configuration
# These environment variables are read by the MySQL container
# They configure the database when it first starts up
ENV MYSQL_ROOT_PASSWORD=root  # Set the root user password
ENV MYSQL_DATABASE=user_db    # Automatically create a database called user_db
                               # This is convenient - don't have to create it manually!

# Expose MySQL default port
# Port 3306 is the standard MySQL port
# EXPOSE documents that this container uses port 3306
# The actual port mapping (3306:3306) is in docker-compose.yml
# This allows me to connect to MySQL from my host machine using localhost:3306
EXPOSE 3306