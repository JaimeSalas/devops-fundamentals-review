FROM node:14-alpine as base 
RUN mkdir -p /usr/src/app 
WORKDIR /usr/src/app 

FROM base AS build-app 
RUN mkdir -p /usr/src/build-app 
WORKDIR /usr/src/build-app
COPY ./package*.json ./
RUN npm ci 
COPY ./ ./  
RUN npm run build 

FROM base AS release 
COPY --from=build-app /usr/src/build-app/dist ./ 

COPY ./package*.json ./
RUN npm ci --only=production 

ENTRYPOINT [ "node", "./index.js" ]
