    FROM node:22-alpine AS quality
    WORKDIR /src
    COPY . .
    RUN npm i -g prettier \
     && prettier --check "**/*.{js,css,html}"

    #stage: runtime
    FROM nginx:alpine
    COPY --from=quality /src /usr/share/nginx/html
    EXPOSE 80
