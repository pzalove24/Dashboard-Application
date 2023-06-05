# ==== CONFIGURE =====
# Use a Node 18 base image
FROM node:18-alpine AS builder
ENV NODE_ENV development
WORKDIR /app
# Copy app files
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000

CMD ["npm", "start"]