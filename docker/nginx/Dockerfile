# The first stage
# Build React static files
FROM node:13.12.0-alpine as build

WORKDIR /app/front
COPY ./front/package.json ./
COPY ./front/package-lock.json ./
RUN npm install -g npm@latest
RUN npm ci --silent
COPY ./front/ ./
RUN npm run build

# The second stage
# Copy React static files and start nginx
FROM nginx:stable-alpine
COPY --from=build /app/front/build /usr/share/nginx/html
CMD ["nginx", "-g", "daemon off;"]