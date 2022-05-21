pipeline { 

    environment {  

    }

    agent any 

    stages { 

        stage('Cloning our Git') { 

            steps { 

                git 'https://github.com/NewthingAde/Udagram-Image-Filtering-Microservice' 

            }

        } 

        stage('Building our image') { 

            steps { 

                script { 

                    
                    sh 'docker build -t udagram-api-feed ./udagram-api-feed:latest .' 
                    sh 'docker tag udagram-api-feed newthingade/udagram-api-feed:latest'
                    sh 'docker tag udagram-api-feed newthingade/udagram-api-feed:$BUILD_NUMBER'
                    
                    sh 'docker build -t udagram-api-user ./udagram-api-user:latest .' 
                    sh 'docker tag udagram-api-user newthingade/udagram-api-user:latest'
                    sh 'docker tag udagram-api-user newthingade/udagram-api-user:$BUILD_NUMBER'
                    
                    sh 'docker build -t udagram-frontend ./udagram-frontend:latest .' 
                    sh 'docker tag udagram-frontend newthingade/udagram-frontend:latest'
                    sh 'docker tag udagram-frontend newthingade/udagram-frontend:$BUILD_NUMBER'
                   
                    
                    sh 'docker build -t udagram-reverseproxy ./udagram-reverseproxy:latest .' 
                    sh 'docker tag udagram-reverseproxy newthingade/udagram-reverseproxy:latest'
                    sh 'docker tag udagram-reverseproxy newthingade/udagram-reverseproxy:$BUILD_NUMBER'
                   
                   

                }

            } 

        }



        stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
          sh  'docker push newthingade/udagram-api-feed:latest'
          sh  'docker push newthingade/udagram-api-feed:$BUILD_NUMBER' 

          sh  'docker push newthingade/udagram-api-user:latest'
          sh  'docker push newthingade/udagram-api-user:$BUILD_NUMBER' 

          sh  'docker push newthingade/udagram-frontend:latest'
          sh  'docker push newthingade/udagram-frontend:$BUILD_NUMBER' 

          sh  'docker push newthingade/udagram-reverseproxy:latest'
          sh  'docker push newthingade/udagram-reverseproxy:$BUILD_NUMBER' 

        }
                  
          }
        }

    }

}