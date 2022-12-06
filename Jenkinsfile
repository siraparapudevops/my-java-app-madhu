
pipeline {
   agent any
   stages {
      stage("getVersion"){
         steps {
            script {
               def pom = readMavenPom file: 'pom.xml'
               echo "Version: ${pom.version}"
            }
            
         }
      }
   
   }
}
