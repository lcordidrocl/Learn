FROM node

WORKDIR /backend

COPY package.json /backend

RUN npm install

COPY . /backend

EXPOSE 80

CMD ["node", "app.js"]