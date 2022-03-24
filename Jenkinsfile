pipeline
{ environment 
 registryCredential = "dockerhub_credentials" 

    imagenameback = "abeerab/backimage:latest" 
    dockerImageback = 'image-back' 
    imagenamefront = "abeerab/firstimage:latest" 
    dockerImagefront = 'image-front' 
    imagenamemongo = "abeerab/db" 
    dockerImagemongo = 'mongo'
// scannerHome = tool name: 'sonarqube-scanner' } 
agent any
 stages { 
        
   
       
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
                dockerImagemongo.push("$BUILD_NUMBER") dockerImagemongo.push('4.2.0')



            } 
        } 
    } 
}  
     stage('Deploy App') { 
          
       { steps { withCredentials([ string(credentialsId: 'my_kubernetes', variable: 'api_token') ]) {
     
          sh 'kubectl --token $api_token --server http://localhost:9000/ --insecure-skip-tls-verify=true apply -f ./Kubernetes '  
       }
    }
   } 
 }

     







