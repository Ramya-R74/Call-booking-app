#FROM node:17.9.0-slim
#LABEL maintainer="Ramya R"
#RUN useradd adminapi
#WORKDIR /app
#RUN chown adminapi /app /home
#COPY . .
#RUN npm install 
#EXPOSE 1004
#USER adminapi
#ENV MONGO_URL=""
#CMD ["npm","start"]

######### new docker file ##############
# Use an official Node.js LTS slim image for stability and smaller size
FROM node:lts-slim

# Add metadata
LABEL maintainer="Ramya R"

# Create a non-root user and set permissions
RUN useradd -m -s /bin/bash adminapi && \
    mkdir -p /app && \
    chown -R adminapi:adminapi /app

# Set working directory
WORKDIR /app

# Copy only package.json and package-lock.json to leverage Docker caching
COPY package*.json ./

# Install dependencies
RUN npm install --production

# Copy application files
COPY . .

# Ensure proper permissions for the non-root user
RUN chown -R adminapi:adminapi /app

# Switch to non-root user
USER adminapi

# Expose the application's port
EXPOSE 1004

# Set environment variables with defaults (these can be overridden at runtime)
ENV MONGO_URL=""

# Run the application
CMD ["npm", "start"]

