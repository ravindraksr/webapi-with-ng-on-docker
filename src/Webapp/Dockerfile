FROM nginx:alpine AS base
COPY src/Webapp/_nginx/default.conf /etc/nginx/conf.d/default.conf
WORKDIR /app
EXPOSE 80

FROM node:alpine AS build
WORKDIR /src
COPY src/Webapp/package.json .
RUN npm i -g yarn
RUN yarn

FROM build AS publish
WORKDIR /src
COPY src/src .
RUN npm run build

FROM base AS final
WORKDIR /app
COPY --from=publish /src/dist .
