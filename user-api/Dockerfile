#FROM node:17.9.0-slim
#LABEL maintainer="Ramya R"
#RUN useradd userapi
#WORKDIR /app
#RUN chown userapi /app /home
#COPY . .
#RUN npm install 
#EXPOSE 1004
#USER userapi
#ENV MONGO_URL=""
#ENV ADMIN_EMAIL=""
#CMD ["npm","start"]

########## new docker file ###########
# Use a stable LTS Node.js version
FROM node:lts-slim

# Metadata
LABEL maintainer="Ramya R"

# Create non-root user and set permissions
RUN useradd -m -s /bin/bash userapi && \
    mkdir /app && \
    chown -R userapi:userapi /app

# Set working directory
WORKDIR /app

# Copy only package.json and install dependencies
COPY package*.json ./
RUN npm install --production

# Copy the rest of the application
COPY . .

# Set permissions for the app folder
RUN chown -R userapi:userapi /app

# Switch to non-root user
USER userapi

# Set environment variables
ENV MONGO_URL=""
ENV ADMIN_EMAIL=""

# Expose the app's port
EXPOSE 1004

# Start the application
CMD ["npm", "start"]

