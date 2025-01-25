#FROM node:17.9.0-slim
#LABEL maintainer="Ramya R"
#RUN useradd userui
#WORKDIR /app
#RUN chown userui /app /home
#COPY . .
#RUN npm install 
#EXPOSE 3000
#USER userui
#CMD ["npm","start"]

######## Updated Dockerfile ###########
# Use an official Node.js LTS slim image for stability and better support
FROM node:lts-slim

# Add metadata for maintainability
LABEL maintainer="Ramya R"

# Create a non-root user and set up the working directory
RUN useradd -m -s /bin/bash userui && \
    mkdir -p /app && \
    chown -R userui:userui /app

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json to leverage Docker's caching
COPY package*.json ./

# Install dependencies
RUN npm install --production

# Copy the rest of the application code
COPY . .

# Ensure proper ownership for the non-root user
RUN chown -R userui:userui /app

# Switch to the non-root user
USER userui

# Expose the application's port
EXPOSE 3000

# Run the application
CMD ["npm", "start"]

