FROM node:14-slim

WORKDIR /app

COPY package*.json ./

RUN npm ci --only=production

COPY . .

RUN useradd -r -s /bin/false -u 1001 nodeuser && chown -R nodeuser:nodeuser /app

USER nodeuser

EXPOSE 8081

CMD ["node", "server.js"]
