pipeline {
   agent any

    tools { 
        maven 'MAVEN'
    }
   
   environment {
     ORGANIZATION_NAME = "dindo-manondo"
     YOUR_DOCKERHUB_USERNAME = "dindo"
     SERVICE_NAME = "fleetman-api-gateway"
     REPOSITORY_TAG="${YOUR_DOCKERHUB_USERNAME}/${ORGANIZATION_NAME}-${SERVICE_NAME}:${BUILD_ID}"
   }

   stages {
      stage('Preparation') {
         steps {
            cleanWs()
            git credentialsId: 'github', url: "https://github.com/${ORGANIZATION_NAME}/${SERVICE_NAME}"
         }
      }
      stage('Build') {
         steps {
            // sh '''mvn clean package'''
            sh '''
            echo "Maven building"
            mvn -v
            '''
         }
      }

      stage('Build and Push Image') {
         steps {
           // sh 'docker image build -t ${REPOSITORY_TAG} .'
            sh '''
            echo "Docker build and docker push"
            mvn -v
            '''
         }
      }

      stage('Deploy to Cluster') {
          steps {
                    // sh 'envsubst < ${WORKSPACE}/deploy.yaml | kubectl apply -f -'
               sh '''
               echo "Deploying to the cluster"
               mvn -v
               '''
          }
      }
   }
}
