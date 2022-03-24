pipeline{
    environment {
        imagename = "abeerab/backimage"
        registryCredential = "dockerhub_credentials"
        scannerHome = tool name: 'sonarqube-scanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
        // scannerHome = tool 'sonarqube-scanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'

    }
    agent any
    stages{
        stage("test-sonar"){
            steps{
                script {
                    withSonarQubeEnv("sonarQube") {
                    sh "${scannerHome}/bin/sonar-scanner \
                        -Dsonar.projectKey=mern-app\
                        -Dsonar.sources=. \
                        -Dsonar.host.url=http://15.236.24.79:9000/ \
                        -Dsonar.login=admin \
                        -Dsonar.password=admin"
                    } 
                }
            }
        }
        stage("install dependencies"){

            steps{
                sh 'npm install'
            }
        }

        stage("docker-build"){
            steps{
                script {
                    dockerImage = docker.build imagename
                    docker.withRegistry( '', registryCredential ) {
                    dockerImage.push("$BUILD_NUMBER")
                    dockerImage.push('latest')
                    }
                }
            }
        }
}
