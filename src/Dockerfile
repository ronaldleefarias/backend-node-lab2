## Dockerfile cration
FROM node:22 AS build

WORKDIR /usr/app

COPY ./ /usr/app

RUN npm install
RUN npm run lint
RUN npm run test:cov
RUN npm run build

FROM node:22-alpine
WORKDIR /usr/app
COPY --from=build /usr/app/dist ./dist
COPY --from=build /usr/app/package*.json .
RUN npm install --only=production

EXPOSE 4000
CMD ["node", "dist/main.js"]