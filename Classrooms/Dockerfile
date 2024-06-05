# Use the official Node.js image as the base image
FROM node:14

# Set the working directory inside the container
WORKDIR /auth

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install the dependencies
RUN npm install

# Copy the rest of the application code to the working directory
COPY . .

# Expose the port the backend API runs on
EXPOSE 11681

# Start the application
CMD ["node", "index.js"]
