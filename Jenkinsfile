pipeline {

      agent any
      environment {
            registry = "pramdoc/kproject"
            registryCredential = 'Docker'
      }
      stages{
        stage('Build') {
          steps{
            bat 'mvn clean package'
          }
        }
        

        
        stage('Building image') {
          steps{
                script {
                      dockerImage= docker.build registry + ":$BUILD_NUMBER"
                }
           }
         }
            
         stage('Push image to dockerhub') {
      
               withDockerRegistry([ credentialsId: "Docker", url: "" ]){
                     bat "docker push pramdoc/kproject:%BUILD_NUMBER%"
               }
         }
      }
}
