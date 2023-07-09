FROM node:20.3.1

WORKDIR /app

COPY server.js server.js

RUN npm install ws

ENTRYPOINT [ "node", "server.js" ]