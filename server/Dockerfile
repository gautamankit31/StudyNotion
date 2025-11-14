# FROM ubuntu:latest

# RUN apt-get update -y
# RUN apt-get install -y curl
# RUN curl -sL https://deb.nodesource.com/setup_16.x | bash -
# RUN apt-get upgrade -y
# RUN apt-get install -y nodejs npm

# WORKDIR /user/server

# COPY package* .

# RUN npm install

# COPY . .

# EXPOSE 4000

# CMD ["npm", "run", "start"]

# Use official Node image
FROM node:18-alpine

# Set working directory
WORKDIR /app

# Copy only package.json first
COPY package*.json ./

# Install dependencies
# RUN npm install

# use CI for reproducible installs (installs prod+dev if package-lock requires)
RUN npm ci --only=production

# Copy all files
COPY . .

# Expose backend port
ENV NODE_ENV=production
EXPOSE 4000

# Start backend
CMD ["npm", "run", "start"]


# docker build -t studynotion-backend .  
# docker run -d -p 4000:4000 --name studynotion-backend --env-file .env studynotion-backend