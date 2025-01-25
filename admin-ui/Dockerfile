#FROM node:17.9.0-slim
#LABEL maintainer="Ramya R"
#RUN useradd adminui
#WORKDIR /app
#RUN chown adminui /app /home
#COPY . .
#RUN npm install 
#EXPOSE 3000
#USER adminui
#CMD ["npm","start"]

########### Updated Dockerfile ##############
# Use a stable Node.js LTS slim image for reliability and performance
FROM node:lts-slim

# Add metadata
LABEL maintainer="Ramya R"

# Create a non-root user and set permissions for the application directory
RUN useradd -m -s /bin/bash adminui && \
    mkdir -p /app && \
    chown -R adminui:adminui /app

# Set the working directory
WORKDIR /app

# Copy only package files to leverage Docker caching during dependency installation
COPY package*.json ./

# Install dependencies
RUN npm install --production

# Copy the rest of the application code
COPY . .

# Ensure proper ownership for the non-root user
RUN chown -R adminui:adminui /app

# Switch to the non-root user
USER adminui

# Expose the application's port
EXPOSE 3000

# Start the application
CMD ["npm", "start"]

