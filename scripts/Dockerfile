
FROM alpine:3.16 as code
WORKDIR /code
RUN apk add --no-cache git && \
    git clone https://github.com/LaughingGor/sub-web --depth=1

# ---- Dependencies ----
FROM node:16-alpine AS build
COPY --from=code /code/sub-web /app
WORKDIR /app
RUN yarn install && \
    yarn build

FROM nginx:1.16-alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD [ "nginx", "-g", "daemon off;" ]
