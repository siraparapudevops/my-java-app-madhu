pipeline {
   agent any
   stages{


   //  stage("Get All Vars"){
   //    steps {
   //       printenv
   //    }
   //  }  

    stage("Build Code"){
      steps {
         script {
            sh """
            mvn install
            mv target/*.war target/myApp-${BUILD_NUMBER}.war
            """


         }
      }
    }
    stage("Code Analysis"){
      steps {
         script {
            sh "/opt/sonar/bin/sonar-scanner -Dproject.settings=./myjavaapp.properties"
         }
      }
    }

    stage ('Upload Artifacts') {
            steps {
               rtUpload (
                    // Obtain an Artifactory server instance, defined in Jenkins --> Manage Jenkins --> Configure System:
                    serverId: myjfroginstance,
                    spec: """{
                            "files": [
                                    {
                                        "pattern": "target/*.war",
                                        "target": "example-repo-local"
                                    }
                                ]
                            }"""
               )
            }
        }

   }
}
