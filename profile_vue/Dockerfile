FROM node:22

WORKDIR /app

COPY . .

RUN npm install

RUN npm run build

EXPOSE 8080
CMD ["npm", "run", "dev"]
