# Base Build
FROM node:16-alpine as builder

# Working Dir
USER node
 
RUN mkdir -p /home/node/app
WORKDIR /home/node/app

# Copy 
COPY --chown=node:node ./package.json ./
RUN npm install
COPY --chown=node:node . .
RUN npm run build

# Base Container
FROM nginx
EXPOSE 3000
COPY ./ngnix/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /home/node/app/build /usr/share/nginx/html