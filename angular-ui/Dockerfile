# Dockerfile for Angular App
FROM node:18 as build

WORKDIR /angular-ui

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application
COPY . .

# Build the application
RUN npm run build -- --configuration=production


# Production stage
FROM nginx:alpine

# Copy the build output to replace the default nginx contents
COPY --from=build /angular-ui/dist/sre-app/browser /usr/share/nginx/html



# Copy our custom nginx config
COPY nginx.conf /etc/nginx/conf.d/default.conf


EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]



