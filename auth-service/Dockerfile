# Используем базовый образ Go
FROM golang:1.20 AS builder

# Установим рабочую директорию
WORKDIR /app

# Копируем go.mod и go.sum для загрузки зависимостей
COPY go.mod go.sum ./

# Загружаем зависимости
RUN go mod download

# Копируем весь исходный код
COPY . .

# Собираем приложение
RUN go build -o auth-service .

# Используем легкий образ для финальной сборки
FROM alpine:latest

WORKDIR /root/

# Копируем скомпилированное приложение
COPY --from=builder /app/auth-service .

# Запускаем приложение
CMD ["./auth-service"]
