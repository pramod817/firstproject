pipeline {

      agent any
      environment {
            registry = "pramdoc/kproject"
            registryCredential = 'Docker'
            dockerImage = ''
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
            
         stage('Deploy our image') {
steps{
script {
docker.withRegistry( '', registryCredential ) {
dockerImage.push()
}
}
}
      }
}
