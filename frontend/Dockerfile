# Estágio 1: compila a aplicação Angular
FROM node:20-alpine AS builder
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm ci
COPY . .
RUN npm run build

# Estágio 2: imagem final, apenas com Nginx servindo os arquivos compilados
FROM nginx:alpine AS runner
COPY --from=builder /app/dist/todo-frontend/browser /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
