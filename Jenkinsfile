pipeline {

      agent any
     
      stages{
        stage('Build') {
          steps{
            bat 'mvn clean package'
          }
        }
        
        stage('SonarQube analysis') {
          steps{
            withSonarQubeEnv('sonarqube') { 
              bat 'mvn sonar:sonar'
            }
          }
        }
        
        stage ('Artifactory') {
          steps {
            rtUpload (
              serverId: 'jfrog', 
                spec: """{
                  "files": [
                    {
                      "pattern": "*/*.war",
                      "target": "firstproject/"
                    }
                  ]
                }"""
            )
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

 
bat "docker push vkgarg/vinit:%BUILD_NUMBER%"

 
}

 
}
      }
}
