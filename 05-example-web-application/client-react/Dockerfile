FROM node:24-bookworm AS build

WORKDIR /usr/src/app

COPY package*.json ./

RUN --mount=type=cache,target=/usr/src/app/.npm \
  npm set cache /usr/src/app/.npm && \
  npm ci

COPY . .

RUN npm run build

###
FROM nginxinc/nginx-unprivileged:alpine3.21-perl

COPY nginx.conf /etc/ngins/conf.d/default.conf

COPY --from=build usr/src/app/dist /usr/share/nginx/html

EXPOSE 8080
