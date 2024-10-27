# Используем официальный образ Go 1.21 для сборки
FROM golang:1.21-alpine AS builder

WORKDIR /app

# Копируем файлы go.mod и go.sum и устанавливаем зависимости
COPY go.mod go.sum ./
RUN go mod download

# Копируем остальной исходный код
COPY . .

# Собираем бинарник
RUN go build -o auth-service

# Минимальный образ для запуска
FROM alpine:latest

WORKDIR /app

# Копируем бинарник из предыдущего этапа
COPY --from=builder /app/auth-service .

# Устанавливаем переменные окружения
ENV CGO_ENABLED=0

# Команда по умолчанию для запуска контейнера
CMD ["./auth-service"]
