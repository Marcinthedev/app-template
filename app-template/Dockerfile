# Przykład dla apki Node (Next.js, Express itp.). Apka nasłuchuje na porcie 3000.
FROM node:22-slim AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build --if-present

FROM node:22-slim
WORKDIR /app
ENV NODE_ENV=production PORT=3000
COPY --from=build /app ./
EXPOSE 3000
CMD ["npm", "start"]
