# Stage 1: Build React app
FROM node:14 AS build

WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Stage 2: Serve app with nginx
FROM nginx:alpine

# Copy custom nginx configuration file
COPY nginx.conf /etc/nginx/nginx.conf

# Copy build output from the previous stage
COPY --from=build /usr/src/app/build /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
