# build env
FROM node:9.1-alpine as build-env
WORKDIR /app

COPY package.json ./
COPY package-lock.json ./

RUN npm i

COPY src ./
COPY tsconfig.json ./

RUN npm run build-prod

# runtime env
FROM node:9.1-alpine

WORKDIR /app
COPY package.json ./
COPY package-lock.json ./

RUN npm i --production

COPY --from=build-env /app/dist ./

CMD ["npm", "run", "server"]
