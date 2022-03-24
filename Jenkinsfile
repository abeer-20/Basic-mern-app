pipeline
{ environment 
{ registryCredential = "dockerhub_credentials" 

    imagenameback = "abeerab/backimage:latest" 
    dockerImageback = 'image-back' 
    imagenamefront = "oussama24/frontendapp:latest" 
    dockerImagefront = 'image-front' 
    imagenamemongo = "abeerab/firstimage:latest" 
    dockerImagemongo = 'mongo'
// scannerHome = tool name: 'sonarqube-scanner' } 
agent any
 stages { 
       stage('scan') {
          steps {
             withSonarQubeEnv(installationName: 'SonarQube') {
              sh './mvnw clean org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.0.2155:sonar'
        }
      }
   }
       
       stage('SonarQube analysis') {
           steps { 
             script {
                scannerHome = tool name: 'SonarScanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation' withSonarQubeEnv('sonarqube-server') {
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

     stage("docker-build") { 
           steps { 
               script { 
                 dockerImageback = docker.build imagenameback docker.withRegistry( '', registryCredential ) { 
                 dockerImageback.push("$BUILD_NUMBER") dockerImageback.push('latest') 
             } 
           } 
            script { dockerImagefront = docker.build imagenamefront docker.withRegistry( '', registryCredential ) { 
                 dockerImagefront.push("$BUILD_NUMBER") dockerImagefront.push('latest') 
             } 
             } 
                script { dockerImagemongo = docker.build imagenamemongo docker.withRegistry( '', registryCredential ) { 
                dockerImagemongo.push("$BUILD_NUMBER") dockerImagemongo.push('latest')



            } 
        } 
    } 
}  
   stage('Deploy App') { 
          steps {
        echo 'deploying the application ...'



     }
    }
  }
} 

