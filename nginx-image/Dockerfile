FROM nginx:latest

# Instalar ping e curl (requisito do projeto)
RUN apt-get update && apt-get install -y iputils-ping curl

# Copiar configuração personalizada
COPY nginx.conf /etc/nginx/nginx.conf

# Expor porta 8080 (para load balancer)
EXPOSE 8080