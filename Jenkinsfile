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
            
         stage('Push image') {
         withCredentials([usernamePassword( credentialsId: 'Docker', usernameVariable: 'USER', passwordVariable: 'PASSWORD')]) {
        def registry_url = "registry.hub.docker.com/"
        bat "docker login -u $USER -p $PASSWORD ${registry_url}"
        docker.withRegistry("http://${registry_url}", "Docker") {
            // Push your image now
            bat "docker push pramdoc/kproject:%BUILD_NUMBER%"
        }
    }
}
      }
}
