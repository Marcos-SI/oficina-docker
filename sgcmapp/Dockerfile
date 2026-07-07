FROM node:18-alpine
WORKDIR /app

# Copia apenas os arquivos de dependência primeiro (melhora o cache do Docker)
COPY package*.json ./

# Aumenta a tolerância de rede do npm e instala as dependências
RUN npm config set fetch-retries 5 && \
    npm config set fetch-retry-mintimeout 20000 && \
    npm config set fetch-retry-maxtimeout 120000 && \
    npm install

# Copia o resto do código do projeto
COPY . .

EXPOSE 4200

# Nota: O comando de inicialização real ("npm start...") está definido no docker-compose.yml