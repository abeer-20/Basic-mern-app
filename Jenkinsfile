pipeline {
  
   agent any
   parameters {
       string (name:'VERSION', defaultvalue: '', description:'version to deploy on prod') 
   }
   tools {
       NodeJS 'node 16.14.1'
   }
  stages {
    stage("build") {
      steps {
        echo 'building the application ...'
        sh "npm install"
      }
    } 
    stage("test") {
      steps {
        echo 'testing the application ...'
      }
    }
    stage("deploy") {
      steps {
        echo 'deploying the application ...'
      }
    }
  }
} 
