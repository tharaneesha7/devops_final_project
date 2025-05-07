# Use official Node.js image
FROM node:latest

# Set working directory
WORKDIR /app

# Copy package files first for better caching
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy all other files
COPY . .

# Expose port
EXPOSE 3000

# Start command
CMD ["npm", "run", "dev"]