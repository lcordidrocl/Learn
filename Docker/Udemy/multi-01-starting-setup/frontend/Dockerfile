FROM node

WORKDIR /ui

COPY package.json /ui

RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]