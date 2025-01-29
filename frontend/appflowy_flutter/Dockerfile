FROM cirrusci/flutter:stable AS build

WORKDIR /app
COPY . .

RUN flutter pub get
RUN flutter build web

# Estágio de produção
FROM node:14-alpine AS production

WORKDIR /app
COPY --from=build /app/build/web /app

RUN npm install -g http-server

EXPOSE 8080
CMD ["http-server", "/app", "-p", "8080", "--host", "0.0.0.0"]
