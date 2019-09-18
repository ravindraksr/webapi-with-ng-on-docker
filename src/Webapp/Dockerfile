FROM nginx:alpine AS base
WORKDIR /wwwroot
EXPOSE 80

FROM node:alpine AS stage
RUN npm i -g yarn
WORKDIR /source
COPY src/Webapp/package.json .
RUN yarn

FROM stage AS build
COPY src/Webapp .
RUN npm run build

FROM base AS final
COPY --from=build /source/dist .
COPY --from=build /source/_nginx/default.conf /etc/nginx/conf.d/default.conf
