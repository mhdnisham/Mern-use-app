FROM node:20-alpine 

WORKDIR /app

COPY packages*.json ./

RUN npm install --only=production

COPY . .

EXPOSE 5000

CMD [ "npm", "start" ]