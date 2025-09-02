# react-frontend/Dockerfile

    FROM node:20-alpine AS build
    WORKDIR /app
    
    COPY package*.json ./
    
    RUN npm ci --include=dev
    
    COPY . .
    RUN npm run build
    
    FROM nginx:stable-alpine
    
    RUN apk add --no-cache curl
    
    COPY nginx.conf /etc/nginx/conf.d/default.conf
    
    COPY --from=build /app/dist /usr/share/nginx/html
    
    EXPOSE 80
    
    HEALTHCHECK CMD curl -fsS http://localhost/ >/dev/null || exit 1
    