FROM node:alpine
WORKDIR '/app'
COPY ./package.json ./
RUN npm install
COPY . .
RUN npm run build
#npm run build will generate necessary files to run react app on production server
#which will be the following nginx server
FROM nginx
#The EXPOSE instruction does not actually publish the port. It functions as a type of documentation between the person who builds the image and the person who runs the container, about which ports are intended to be published. To actually publish the port when running the container, use the -p flag on docker run to publish and map one or more ports, or the -P flag to publish all exposed ports and map them to high-order ports.
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
#copy those files generated from the first stage over to this folder for nginx to host them
COPY --from=0 /app/build /usr/share/nginx/html