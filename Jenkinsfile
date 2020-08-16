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
                     def registry_url = "registry.hub.docker.com/" 
                     def user = "pramdoc"
                     def pass = "pramodchaturedi"
                     bat "docker login -u ${user} -p ${pass} ${registry_url}"
                     bat "docker push pramdoc/kproject:%BUILD_NUMBER%"
               }
         }
      }
}
