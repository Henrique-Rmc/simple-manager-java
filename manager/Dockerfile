# --- Estágio 1: Build (Usando imagem oficial do Gradle) ---
FROM gradle:8-jdk17 AS build
WORKDIR /app
COPY . .
# O comando 'gradle bootJar' cria o .jar executável
# O '-x test' pula os testes para agilizar este primeiro deploy
RUN gradle bootJar --no-daemon -x test

# --- Estágio 2: Execução (Imagem leve apenas com Java) ---
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
# Copia o jar gerado no estágio anterior.
# O Gradle costuma salvar em /build/libs/
COPY --from=build /app/build/libs/*.jar app.jar

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]