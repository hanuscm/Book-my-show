# Use Node.js 18 (or your Jenkins-configured version)
FROM node:18-bullseye

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package.json package-lock.json ./

# Force install a compatible PostCSS version to fix the issue
RUN npm install postcss@8.4.21 postcss-safe-parser@6.0.0 --legacy-peer-deps
#RUN npm install postcss@latest postcss-flexbugs-fixes@latest postcss-preset-env@latest react-scripts@latest --legacy-peer-deps

# Install dependencies
RUN npm install --force  # Install fresh dependencies
RUN npm audit fix --force & sleep 10 & sleep 100 & npm audit fix --force & sleep 100 & npm fund

# Copy the entire project
COPY . .

# Expose port 3000
EXPOSE 1000

# Set environment variable to prevent OpenSSL errors
ENV NODE_OPTIONS=--openssl-legacy-provider
ENV PORT=3000

# Start the application
CMD ["npm", "start"]
