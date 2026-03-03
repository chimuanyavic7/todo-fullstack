# ========================
# Stage 1: Build
# ========================
FROM node:20-alpine AS build

WORKDIR /app

# Copy package.json first for caching
COPY package.json ./

# Install all dependencies (dev + prod) for build
RUN npm install

# Copy source code
COPY . .

# Remove this line if your app does not need a build
# RUN npm run build

# ========================
# Stage 2: Production
# ========================
FROM node:20-alpine AS production

WORKDIR /app

# Copy package.json for installing only production dependencies
COPY package.json ./

# Install only production dependencies
RUN npm install --production

# Copy all app files from build stage
COPY --from=build /app ./

# Set environment
ENV NODE_ENV=production

# Expose the port your app listens on
EXPOSE 3000

# Start the app
CMD ["node", "server.js"]