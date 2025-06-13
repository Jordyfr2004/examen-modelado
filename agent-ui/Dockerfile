# Etapa 1: Construcción
FROM node:20 AS builder

# Establece directorio de trabajo
WORKDIR /app

# Copia los archivos de definición de dependencias
COPY agent-ui/package*.json ./

# Instala dependencias
RUN npm install

# Copia el resto del código
COPY agent-ui .

# Compila la app
RUN npm run build

# Etapa 2: Producción
FROM node:20 AS runner

WORKDIR /app

ENV NODE_ENV=production

# Copiar artefactos del build desde la etapa anterior
COPY --from=builder /app/public ./public
COPY --from=builder /app/.next ./.next
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/package.json ./package.json

EXPOSE 8080
ENV PORT=8080

# Comando para arrancar la app en producción
CMD ["npm", "start"]
