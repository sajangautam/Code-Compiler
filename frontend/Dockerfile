# Stage 1: Build the React app
FROM node:14-alpine as build

WORKDIR /app

COPY package.json ./
COPY package-lock.json ./

RUN npm install

COPY . ./

# Fix the permission issue
RUN chmod +x node_modules/.bin/react-app-rewired

RUN npm run build

# Stage 2: Serve the React app using nginx
FROM nginx:alpine

COPY --from=build /app/build /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
