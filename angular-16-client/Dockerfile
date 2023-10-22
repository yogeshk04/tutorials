# Stage 1: Build the application

FROM node:18-alpine3.18 as build
WORKDIR /app
COPY package*.json /app/
RUN npm install
RUN npm install -g @angular/cli@16.0.2
COPY . /app/
RUN ng build --configuration production

# Stage 2: Create a lightweight image for running the application
FROM nginx:1.25.2-alpine
# COPY default.conf /etc/nginx/conf.d/default.conf
COPY --from=build /app/dist/angular-16-crud /usr/share/nginx/html
EXPOSE 4200
CMD [ "nginx", "-g", "daemon off;" ]