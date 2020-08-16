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
      
               steps{
                     bat "docker login --username 'pramdoc' --password 'pramodchaturvedi'"
                     bat "docker push pramdoc/kproject:%BUILD_NUMBER%"
               }
         }
      }
}
