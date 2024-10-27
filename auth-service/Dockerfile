# Dockerfile для auth-service
FROM golang:1.20-alpine

WORKDIR /app

# Копируем и устанавливаем зависимости
COPY go.mod ./
COPY go.sum ./
RUN go mod download

# Копируем остальной код
COPY . .

# Собираем приложение
RUN go build -o auth-service

# Устанавливаем переменные окружения для работы с тестами, если необходимо
ENV CGO_ENABLED=0

# Команда по умолчанию
CMD ["./auth-service"]
