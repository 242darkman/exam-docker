FROM node:20 as builder

WORKDIR /app

COPY package.json pnpm-lock.yaml ./

RUN npm install -g pnpm && pnpm install

COPY . .

RUN pnpm run build

FROM node:20

WORKDIR /app

COPY --from=builder /app/dist ./dist

COPY package.json pnpm-lock.yaml ./

RUN npm install -g pnpm && pnpm install --prod

ENV NODE_ENV production

CMD ["node", "dist/server.js"]

