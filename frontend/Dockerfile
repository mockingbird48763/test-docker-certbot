FROM node:22 AS build-stage

WORKDIR /app

COPY ./package.json /app/package.json
COPY ./package-lock.json /app/package-lock.json

RUN npm install

COPY . .

RUN npm run build

FROM nginx:alpine as production-stage
COPY --from=build-stage /app/dist /usr/share/nginx/html
COPY ./nginx/mockingbird48763.online.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
