FROM node:22-slim

ENV PNPM_HOME="/pnpm"
ENV PATH="$PNPM_HOME:$PATH"
RUN corepack enable

RUN apt-get update -y && apt-get install -y openssl

RUN mkdir -p /home/node/app/node_modules && chown -R node:node /home/node/app

WORKDIR /home/node/app

COPY package.json pnpm-lock.yaml ./

ENV NODE_ENV=production

RUN pnpm install

COPY . .

RUN pnpm generate

COPY --chown=node:node . .

USER node

EXPOSE 3001

CMD [ "pnpm", "dev" ]