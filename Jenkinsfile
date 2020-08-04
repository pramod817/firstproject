pipeline {

      agent any
      tools {
             maven 'maven'
      }
      
      stages{
        stage('Build') {
          steps{
            bat 'mvn package'
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
      }
}
