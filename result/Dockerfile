FROM node:8.9-alpine

WORKDIR /app

COPY . .

RUN npm install -g nodemon && \
    npm config set registry https://registry.npmjs.org && \
    npm install && npm ls && npm cache clean --force && mv /app/node_modules /node_modules

ENV PORT=80

EXPOSE 80

CMD node server.js
