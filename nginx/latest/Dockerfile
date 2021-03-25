FROM nginx:latest

RUN addgroup nobody tty
RUN apk add --no-cache su-exec

CMD [ "su-exec", "nobody", "nginx", "-g", "daemon off;"]
