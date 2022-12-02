pipeline {
   agent any
   stages{

    stage("Build Code"){
      steps {
         script {
            sh "mvn install"
         }
      }
    }
    stage("Code Analysis"){
      steps {
         script {
            sh "/opt/sonar/bin/sonar-scanner -Dproject.settings=./myjavaapp.properties "
         }
      }
    }
   }
}