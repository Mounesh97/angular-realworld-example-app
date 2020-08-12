pipeline {
  environment {
    registry = "mounesh97/conduit"
    registryCredential = 'docker_hub_mounesh97'
    dockerImage = ''
  }
  agent any
  stages{
  
    stage ('Build') {
      steps{
        echo "Building Project"
        
         sh 'npm install'
         sh 'npm run build'
         sh "npm run ng --build  --prod"
        }
      }
    
    
    
    
    stage ('Build Docker Image') {
      steps{
        echo "Building Docker Image"
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage ('Push Docker Image') {
      steps{
        echo "Pushing Docker Image"
        script {
          docker.withRegistry( '', registryCredential ) {
              dockerImage.push()
              dockerImage.push('latest')
          }
        }
      }
    }
     stage ('Deploy to Dev') {
      steps{
        echo "Deploying to Dev Environment"
        sh "docker rm -f conduit || true"
        sh "docker run -d --name=conduit -p 8081:8080 mounesh97/conduit"
      }
    }
  }
}
