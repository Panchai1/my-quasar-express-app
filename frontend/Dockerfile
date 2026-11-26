FROM node:22-alpine AS builder
WORKDIR /app

COPY package*.json ./
RUN npm ci --ignore-scripts

COPY . .
RUN npx quasar prepare
RUN npx quasar build

FROM nginx:1.27-alpine AS runtime
COPY --from=builder /app/dist/spa/ /usr/share/nginx/html/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
