pipeline { 
agent any

 stages { 
       stage('SonarQube analysis') {
           steps { 
             script {
                scannerHome = tool name: 'SonarScanner',
                 type: 'hudson.plugins.sonar.SonarRunnerInstallation' withSonarQubeEnv('sonarqube-server') {
                  sh "${scannerHome}/bin/sonar-scanner" 
              }
              }
            }
    }
      stage("build"){ 

           steps {
             sh 'npm install' 
             sh 'docker --version'
               } 
          }
        
  stage (test sonar"){
         steps{
          script {
           withSonarQubeEnv("sonarQube") {
             sh "${scannerHome}/bin/sonar-scanner\
                        -Dsonar.projectKey=mern-app\
                        -Dsonar.sources=. \
                        -Dsonar.host.url=http://15.236.24.79:9000/\
                        -Dsonar.login=admin \
                        -Dsonar.password=123456789"
           }
                  
          
          }
         
         }
         }
  
  
  
  
  
  
  
 
 }
} 
