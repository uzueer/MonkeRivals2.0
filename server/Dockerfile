FROM node:20-alpine
WORKDIR /app

# Copy package files
COPY package*.json ./
# Install only production dependencies
# This is faster and results in a smaller final image.
RUN npm install --production

# Copy all server source files
COPY . .

# The server is configured to listen on PORT 3000 in server.js
EXPOSE 3000

# The Firebase serviceAccountKey.json is NOT copied here;
# it will be securely mounted as a volume by docker-compose.yml.

# Run the application using the 'start' script defined in package.json
CMD ["npm", "start"]
