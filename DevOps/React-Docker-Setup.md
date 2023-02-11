# Creating a React Docker Container

This readme file describes how to create a docker container for React.js applications.


## Tech and Pre-requisites

- [Docker Runtime] - Docker desktop should be installed.
- [React.JS Application] - A running react.js application


Create a Dockerfile in the root directory of react.js application and paste the below contents in the newly created file.  Below is the file structure of a react.js project containing Dockerfile.

    .
    ├── Dockerfile                   # Dockerfile with Multistaged build
    ├── node_modules                 # Installed modules listed in package.json
    ├── package.json                 # Depedency module with version
    ├── package-lock.json
    ├── src                          # Source files (alternatively `lib` or `app`)
    ├── LICENSE
    └── README.md

### Creating Dockerfile
A *Multistaged build* is used to create a React.JS docker container. First stage is "Build Stage" and other stage is "Production Stage". Benefit of using multistaged build:
"A multi-stage build is a process that allows you to break the steps in building a Docker image into multiple stages. This will enable you to create images that include only the dependencies that are necessary for the desired functionality of the final application, cutting down on both time and space." as described in [Dev.to docs](https://dev.to/pavanbelagatti/what-are-multi-stage-docker-builds-1mi9#:~:text=A%20multi%2Dstage%20build%20is,on%20both%20time%20and%20space.).
Moreover in both the build and production stage we have used "alpine" as base image, that is node:lts-alpine and nginx:stable-alpine as alpine base image is linux based, more secure and very compact.
```sh
# Build Stage
FROM node:lts-alpine as build-stage 
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build     

# Production Stage
FROM nginx:stable-alpine as production-stage
COPY --from=build-stage /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```
### Building the Image
Now the next step is to build the image using docker build command as below:
```sh
docker build -t <docker_id>/<react-app-name>:1.0 .
```
Replace the *<docker_id>* with the docker hub ID and *<react-app-name>* with the name of your react.js application. Example:
```sh
docker build -t raghavsdocker/my_react_app:1.0 .
```
Here *1.0* specifies the version of the application
### Run the Prebuilt Image
To run image using command(select port you want to run, in below case 3000 is selected) 
```sh
docker run --name <name_of_this_container> -p 3000:80 -d raghavsdocker/<react-app-name>:1.0
```

## License

**Free Software, Hell Yeah!**
