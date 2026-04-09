# Build stage
FROM maven:3.9.14 AS builder
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests && \
    mv target/shipping-1.0.jar shipping.jar && \
    rm -rf ~/.m2

# Runtime stage
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
COPY --from=builder /app/shipping.jar .
USER roboshop
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "shipping.jar"]

# FROM maven:3.9.14
# EXPOSE 8080
# WORKDIR /app
# COPY pom.xml .
# COPY src ./src
# RUN mvn clean package 
# RUN mv target/shipping-1.0.jar shipping.jar 
# ENV CART_ENDPOINT="cart:8080" \
#     DB_HOST="mysql"
# CMD ["java", "-jar", "shipping.jar"]