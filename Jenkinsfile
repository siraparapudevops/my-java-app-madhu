
pipeline {
   agent any
   stages {
      stage("getVersion"){
         steps {
            def pom = readMavenPom file: 'pom.xml'
            script {
               
               echo "Version: ${pom.version}"
            }
            
         }
      }
   
   }
}
