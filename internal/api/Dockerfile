# Use uma imagem base do Go
FROM golang:1.22.2 AS builder

# Defina o diretório de trabalho
WORKDIR /app

# Copie o go.mod e go.sum primeiro
COPY ../../go.mod ../../go.sum ./

# Baixe as dependências
RUN go mod download

# Copie o restante do código
COPY . .

# Compile a aplicação
RUN go build -o api ./internal/api/api.go

# Use uma imagem mais leve para rodar o binário
FROM alpine:latest
COPY --from=builder /app/api /app/api

# Adicione permissões de execução ao binário
RUN chmod +x /app/api

# Exponha a porta que a API utiliza
EXPOSE 8080

# Comando para rodar a aplicação
CMD ["/app/api"]
