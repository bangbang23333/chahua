FROM --platform=$BUILDPLATFORM node:22-bookworm AS build

WORKDIR /app

COPY package.json package-lock.json ./
RUN npm ci

COPY . .

ARG CI_BUILD_VERSION
ENV CI_BUILD_VERSION=${CI_BUILD_VERSION}

RUN npm run build:stg

FROM nginx:1.29-alpine

COPY misc/nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80
