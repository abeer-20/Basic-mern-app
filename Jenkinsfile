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
      stage("test-sonar"){
        steps{
          script {
            withSonarQubeEnv("sq1"){
              sh "${scannerHome}/bin/sonar-scanner \
              -Dsonar.projectkey=mern-app\
              -Dsonar.sources=.\
              -Dsonar.host.url=hhtp://localhost:9000/ \
              -Dsonar.login=admin \
              -Dsonar.password=123456789"
            }
          }
        }
      }  
 }
}
