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
 }
}
