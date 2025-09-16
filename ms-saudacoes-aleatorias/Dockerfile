# --- Estágio de Build ---
# Use uma imagem do Go baseada em Alpine. A versão pode ser ajustada.
FROM golang:1.24-alpine AS builder

# Instale as ferramentas de compilação C (gcc, etc.)
# 'build-base' é um meta-pacote que inclui o necessário em Alpine.
RUN apk add --no-cache build-base gcc

# Defina o diretório de trabalho dentro do container
WORKDIR /app

# Copie os arquivos de gerenciamento de dependências primeiro para aproveitar o cache do Docker
COPY go.mod go.sum ./

# Baixe as dependências
RUN go mod download

# Copie o restante do código-fonte da sua aplicação
COPY . .

# Compile a aplicação com CGO habilitado.
# -a: Força a reconstrução de pacotes que estão desatualizados.
# -installsuffix cgo: Evita conflitos entre pacotes CGO e não-CGO.
# O resultado é um binário estaticamente vinculado, que não precisa da libsqlite3.so na imagem final.
RUN CGO_ENABLED=1 GOOS=linux go build -a -installsuffix cgo -o /app/main .

# --- Estágio Final ---
# Define a imagem final, que será muito menor.
# A imagem 'alpine' é uma distribuição Linux mínima, ideal para produção.
FROM alpine:latest

# Define o diretório de trabalho na imagem final.
WORKDIR /app

# Copia o binário compilado do estágio 'builder' para a imagem final.
COPY --from=builder /app/main .

# Copia o banco de dados inicial, se necessário.
# Como o banco de dados 'greetings.db' é criado na primeira execução, não precisamos copiá-lo.
# A aplicação irá criá-lo quando o contêiner iniciar.

# Expõe a porta que a aplicação usa, conforme definido no main.go.
EXPOSE 8080

# Define o comando que será executado quando o contêiner for iniciado.
# Este é o ponto de entrada da nossa aplicação.
CMD ["./main"]
