# Microservices 

![1_V3rlWCItJsmYN97fQ2a3HQ](https://user-images.githubusercontent.com/80678596/177031484-3adf2eba-1c26-4841-953b-306678961395.png)



# Udagram Image Filtering Application

Udagram is a simple cloud application developed alongside the Udacity Cloud Engineering Nanodegree. It allows users to register and log into a web client, post photos to the feed, and process photos using an image filtering microservice.

The project is split into two parts:

1. Frontend - Angular web application built with Ionic Framework
2. Backend RESTful API - Node-Express application

## Getting Started
I started with getting the backend API running since the frontend web application depends on the API.

### Prerequisite
1. The depends on the Node Package Manager (NPM). You will need to download and install Node from [https://nodejs.com/en/download](https://nodejs.org/en/download/). This will allow you to be able to run `npm` commands.

2. Environment variables will need to be set. These environment variables include database connection details that should not be hard-coded into the application code.

#### Environment Script
I used the file named `set_env.sh` to configure my variables on my local development environment.
 
I do _not_ want your credentials to be stored in git. After pulling this `starter` project, I run the following command to tell git to stop tracking the script in git but keep it stored locally. This way, I can use the script for your convenience and reduce risk of exposing your credentials.

`git rm --cached set_env.sh`

Afterwards, I can prevent the file from being included in your solution by adding the file to our `.gitignore` file.

### 1. Database
Create a PostgreSQL database either locally or on AWS RDS. The database is used to store the application's metadata.

* We will need to use password authentication for this project. This means that a username and password is needed to authenticate and access the database.

* The port number will need to be set as `5432`. This is the typical port that is used by PostgreSQL so it is usually set to this port by default.

<img width="1440" alt="Screenshot 2022-05-23 at 20 57 12" src="https://user-images.githubusercontent.com/80678596/169888213-561758aa-271a-4ee9-a154-8008ae70f36e.png">

Once your database is set up, set the config values for environment variables prefixed with `POSTGRES_` in `set_env.sh`.

* If you set up a local database, your `POSTGRES_HOST` is most likely `localhost`

* If you set up an RDS database, your `POSTGRES_HOST` is most likely in the following format: `***.****.us-west-1.rds.amazonaws.com`. You can find this value in the AWS console's RDS dashboard.


### 2. S3
Create an AWS S3 bucket. The S3 bucket is used to store images that are displayed in Udagram.

<img width="1400" alt="Screenshot 2022-05-23 at 21 02 15" src="https://user-images.githubusercontent.com/80678596/169888581-5e713a71-d5a0-4f17-87d4-683b4bc6022a.png">

Set the config values for environment variables prefixed with `AWS_` in `set_env.sh`.

### 3. Backend API
Launch the backend API locally. The API is the application's interface to S3 and the database.

* To download all the package dependencies, run the command from the directory `udagram-api/`:
    ```bash
    npm install .
    
    npm cache clear --force
    ```
* To run the application locally, run:
    ```bash
    npm run dev
    ```
* You can visit `http://localhost:8080/api/v0/feed` in your web browser to verify that the application is running. You should see a JSON payload. Feel free to play around with Postman to test the API's.

<img width="826" alt="Screenshot 2022-05-19 at 14 42 38" src="https://user-images.githubusercontent.com/80678596/169296297-32cb6e4c-ae9f-4b53-bd80-0d7849c5b949.png">

### 4. Frontend App
Launch the frontend app locally.

* To download all the package dependencies, run the command from the directory `udagram-frontend/`:
    ```bash
    npm install .
    ```
* Install Ionic Framework's Command Line tools for us to build and run the application:
    ```bash
     The package name has changed from ionic to @ionic/cli!
                                
             To update, run: npm uninstall -g ionic
             
                 Then run: npm i -g @ionic/cli
    ```
* Prepare your application by compiling them into static files.
    ```bash
    ionic build
    ```
* Run the application locally using files created from the `ionic build` command.
    ```bash
    ionic serve
    ```
* You can visit `http://localhost:8100` in your web browser to verify that the application is running. You should see a web interface.

<img width="730" alt="Screenshot 2022-05-19 at 14 43 05" src="https://user-images.githubusercontent.com/80678596/169296200-ad7a28f6-7f88-45e7-94ef-69551dc56c15.png">


<img width="1167" alt="Screenshot 2022-05-19 at 15 17 23" src="https://user-images.githubusercontent.com/80678596/169302463-804787a2-cc73-4578-bb69-6e57a59c25b8.png">

## Tips
1. Take a look at `udagram-api` -- does it look like we can divide it into two modules to be deployed as separate microservices?
2. The `.dockerignore` file is included for your convenience to not copy `node_modules`. Copying this over into a Docker container might cause issues if your local environment is a different operating system than the Docker image (ex. Windows or MacOS vs. Linux).
3. It's useful to "lint" your code so that changes in the codebase adhere to a coding standard. This helps alleviate issues when developers use different styles of coding. `eslint` has been set up for TypeScript in the codebase for you. To lint your code, run the following:
    ```bash
    npx eslint --ext .js,.ts src/
    ```
    To have your code fixed automatically, run
    ```bash
    npx eslint --ext .js,.ts src/ --fix
    ```
4. `set_env.sh` is really for your backend application. Frontend applications have a different notion of how to store configurations. Configurations for the application endpoints can be configured inside of the `environments/environment.*ts` files.
5. In `set_env.sh`, environment variables are set with `export $VAR=value`. Setting it this way is not permanent; every time you open a new terminal, you will have to run `set_env.sh` to reconfigure your environment variables. To verify if your environment variable is set, you can check the variable with a command like `echo $POSTGRES_USERNAME`.



## Part 2 - Run the project locally in a multi-container environment

The objective of this part of the project is to:


1. Refactor the monolith application to microservices
2. Set up each microservice to be run in its own Docker container

Once you refactor the Udagram application, it will have the following services running internally:

1. Backend /user/ service - allows users to register and log into a web client.

2. Backend /feed/ service - allows users to post photos, and process photos using image filtering.

3. Frontend - It is a basic Ionic client web application that acts as an interface between the user and the backend services.

4. Nginx as a reverse proxy server - for resolving multiple services running on the same port in separate containers. When different backend services are running on the same port, then a reverse proxy server directs client requests to the appropriate backend server and retrieves resources on behalf of the client.

* Navigate to the project directory, and set up the environment variables again
 
    ```bash
    source set_env.sh
    ```
    
* Use Docker compose to build and run multiple Docker containers              

* Create images - In the project's parent directory, create a `docker-compose-build.yaml file` . It will create an image for each individual service. Then, you can run the following command to create images locally then run 

Make sure the Docker services are running in your local machine

Remove unused and dangling images

                 docker image prune --all

Run this command from the directory where you have the "docker-compose-build.yaml" file present

            docker-compose -f docker-compose-build.yaml build --parallel


<img width="849" alt="Screenshot 2022-05-19 at 23 41 00" src="https://user-images.githubusercontent.com/80678596/169410434-a10cb221-812b-4e37-a98d-f5904e69a4b3.png">

Docker images running 

<img width="1315" alt="Screenshot 2022-05-19 at 23 43 31" src="https://user-images.githubusercontent.com/80678596/169410742-223cbc00-c015-4001-982f-56aa73754d44.png">

* Run the container 

                        docker-compose up


* Visit http://localhost:8100 in your web browser to verify that the application is running.



#### Backend api feed

<img width="1438" alt="Screenshot 2022-05-19 at 23 48 41" src="https://user-images.githubusercontent.com/80678596/169410564-d0741e86-f1d3-4593-805c-9c72ebc3f03f.png">



#### Local host server running

<img width="1307" alt="Screenshot 2022-05-19 at 23 44 42" src="https://user-images.githubusercontent.com/80678596/169410840-5818924e-3174-47d1-9ace-903ae0a411d4.png">

#### The containerized application running

<img width="1040" alt="Screenshot 2022-05-19 at 23 45 50" src="https://user-images.githubusercontent.com/80678596/169410923-b241c213-f02b-4123-b9bd-9566d9c8fb6d.png">

<img width="1118" alt="Screenshot 2022-05-19 at 23 47 21" src="https://user-images.githubusercontent.com/80678596/169411009-45d87914-c427-4bf0-ac5d-3c2f142d78ce.png">


#### Images of a succesful build and deploy of docker to dockerhub using Gitlab

<img width="1105" alt="Screenshot 2022-05-22 at 02 40 23" src="https://user-images.githubusercontent.com/80678596/169673602-36b2d64f-3e5c-4965-9575-d07578a4ee31.png">

### Create the HorizontalPodAutoscaler

- Installation

            kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml

- Create the HorizontalPodAutoscaler:(Do this for all deployment)

        kubectl autoscale deployment backend-feed --cpu-percent=70 --min=3 --max=5
        
        kubectl autoscale deployment backend-user --cpu-percent=70 --min=3 --max=5
        
        kubectl autoscale deployment frontend --cpu-percent=70 --min=3 --max=5
        
        kubectl autoscale deployment reverseproxy --cpu-percent=70 --min=3 --max=5
        
- You can check the current status of the newly-made HorizontalPodAutoscaler, by running:

                kubectl get hpa


<img width="892" alt="Screenshot 2022-05-24 at 23 12 44" src="https://user-images.githubusercontent.com/80678596/170134297-dd7c55e5-39b2-4840-9de4-4596e41c9c63.png">
