pipeline {
   agent any
   stages{


    stage ('Artifactory configuration') {
            steps {
                rtServer (
                    id: "artifactory-1",
                    url: "http://172.31.32.31:8082/artifactory",
                    credentialsId: 'jfrog-creds'
                )
            }
    }
    stage("Build Code"){
      steps {
         script {
            sh """
            mvn install
            myver=$(grep -i version pom.xml |head -2 |tail -1|cut -d">" -f2|cut -d"<" -f1)
            mv target/*.war target/myApp-v.${myver}-release${BUILD_NUMBER}".war
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
                    serverId: "artifactory-1",
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
   post {
      always {
         cleanWs()
      }
   }
}
