FROM node:22-trixie

EXPOSE 1980

WORKDIR /front

ARG BACK_URL="http://localhost:8080"
ENV BACK_URL=${BACK_URL}

COPY . .

RUN npm install

CMD npm install && npm start
