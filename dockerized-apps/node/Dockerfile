FROM node:12.21.0-alpine3.12 AS build

WORKDIR /usr/src/app

COPY package*.json /usr/src/app/

RUN npm ci --only=production && rm -f .npmrc

FROM node:12.21.0-alpine3.12

ENV NODE_ENV production

USER node

WORKDIR /usr/src/app

COPY --chown=node:node --from=build /usr/src/app/node_modules /usr/src/app/node_modules

COPY --chown=node:node . /usr/src/app

CMD ["node", "index.js"]