# Etapa 1: Compilación de la aplicación
FROM node:20 AS builder
WORKDIR /app

# Copiar archivos de dependencias e instalarlas
COPY package*.json ./
RUN npm install

# Copiar el resto del código y compilar para producción
COPY . .
RUN npm run build

# Etapa 2: Servidor de producción seguro (Nginx)
# Usamos una imagen de Nginx configurada sin privilegios de root
FROM nginxinc/nginx-unprivileged:alpine

# Copiamos el build generado en la Etapa 1 al directorio de Nginx
COPY --from=builder /app/dist /usr/share/nginx/html

# Exponemos el puerto 8080 (el estándar en la imagen unprivileged)
EXPOSE 8080

# Iniciamos Nginx
CMD ["nginx", "-g", "daemon off;"]