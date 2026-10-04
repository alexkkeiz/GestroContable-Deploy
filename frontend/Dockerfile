FROM node:20-alpine AS build
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm ci
COPY . .
RUN npm run build

RUN mkdir -p /output && \
    if [ -d /app/dist/*/browser ]; then \
        cp -r /app/dist/*/browser/. /output/; \
    else \
        cp -r /app/dist/*/. /output/; \
    fi

FROM nginx:alpine
COPY --from=build /output /usr/share/nginx/html
EXPOSE 80