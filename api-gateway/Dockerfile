# Устанавливаем базовый образ Go
FROM golang:1.21 AS builder

# Устанавливаем рабочую директорию
WORKDIR /app

# Копируем go.mod и go.sum для загрузки зависимостей
COPY go.mod go.sum ./

# Загружаем зависимости
RUN go mod download

# Копируем весь код приложения в контейнер
COPY . .

# Собираем бинарный файл
RUN go build -o api-gateway .

# Используем более легкий образ для финального контейнера
FROM gcr.io/distroless/base

# Копируем бинарный файл из образа сборки
COPY --from=builder /app/api-gateway /api-gateway

# Указываем команду для запуска приложения
ENTRYPOINT ["/api-gateway"]

# Указываем переменную окружения, если необходимо
# ENV MY_ENV_VAR=value
