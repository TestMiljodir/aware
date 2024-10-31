FROM node:lts-alpine AS nodebuilder
WORKDIR /code

COPY --link package.json yarn.lock /code/
RUN yarn install --frozen-lockfile
COPY --link public /code/public
COPY --link src /code/src
RUN yarn build

#stage 2
FROM nginxinc/nginx-unprivileged:stable-alpine-slim
WORKDIR /app
COPY --link --from=nodebuilder /code/build /usr/share/nginx/html
COPY --link /nginx.conf /etc/nginx/nginx.conf

CMD ["nginx", "-g", "daemon off;"]