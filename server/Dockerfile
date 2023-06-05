# Base image

FROM node:18-alpine as base

# Build stage
FROM base
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 5001
CMD [ "index.js" ]