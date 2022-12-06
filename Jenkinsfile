
pipeline {
   agent any
   stages {
      stage("getVersion"){
         steps {
            def pom = readMavenPom file: 'pom.xml'
            echo "Version: ${pom.version}"
         }
      }
   
   }
}
