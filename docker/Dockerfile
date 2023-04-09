#stage build 
FROM node:14-alpine as build
WORKDIR /app
COPY package*.json /app/
RUN npm install
COPY ./ /app/

RUN npm run build
#stage nginx
FROM nginx:1.22.1-alpine
COPY --from=build /app/build/ /usr/share/nginx/html
COPY ./ngnix.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
