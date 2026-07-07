# ETAPA 1: Construção (Build)
# Usa uma imagem pesada que contém o Maven para compilar o código
FROM maven:3.9.9-eclipse-temurin-17 AS build
WORKDIR /workspace

# Copia os arquivos de dependência e baixa o que for necessário
COPY pom.xml ./
COPY .mvn .mvn
COPY src src

# Compila o projeto ignorando os testes para ser mais rápido
RUN mvn -DskipTests package

# ETAPA 2: Execução (Run)
# Usa uma imagem leve só com o Java JRE (não tem Maven, é mais segura e leve)
FROM eclipse-temurin:17-jre
WORKDIR /app

# Pega apenas o arquivo .jar gerado na Etapa 1 e joga fora o resto
COPY --from=build /workspace/target/*.jar app.jar

EXPOSE 9000
ENTRYPOINT ["java", "-jar", "/app/app.jar"]