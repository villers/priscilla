FROM node:14 as prod
WORKDIR /usr/src/app/my-vue-app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build
EXPOSE 3000

CMD ["npm", "run", "serve"]

FROM node:12 as dev
WORKDIR /usr/src/app/my-vue-app
COPY --from=prod /usr/src/app/my-vue-app/ /usr/src/app/my-vue-app/
EXPOSE 3000
CMD ["npm", "run", "dev"]