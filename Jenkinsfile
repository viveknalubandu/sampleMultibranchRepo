def orchestrationToolId = "67d8cfe00f6200109d1a986eb4767e43"
def nexusInstanceId = "localNexus"
def nexusGroupId = "com.globex.web"
def nexusPackaging = "war"
def artifactName = "globex-web1" // also used for nexus filePath and artifactId attributes
def packageName = "globex-package1"
//def artifactUrl = "com.globex.web/globex-web"
def artifactVersion = "1.${env.BUILD_NUMBER}"
//def artifactVersion = "1.40"
//def artifactVersionUrl = "com.globex.web/globex-web/${artifactVersion}/globex-web-${artifactVersion}"
def artifactSemVersion = "${artifactVersion}.0"
//def repoUrl= "ff-artifacts-repo3"
def repoName = "ff-artifacts-repo" // also used for nexusRepositoryId attribute

pipeline {
   agent any
   tools {
      maven 'Maven'
   }
   stages {
       stage("build") {
           steps {
              //snDevOpsStep()
               echo "Building" 
                sh 'mvn clean install -DskipTests'
               //sleep 5
           }
       }
       
     stage("test") {
           stages {
            stage('UAT unit test1') {
                steps {
                     //   snDevOpsStep ()
                        echo "Testing"
                        sh 'mvn -Dtest=com.sndevops.eng.AppTest test'
                   sh 'mvn package'
				//snDevOpsArtifact(artifactsPayload:"""{"artifacts": [{"name": "sa-web-ui.jar2","version":"${artifactVersion}","semanticVersion": "${artifactSemVersion}","repositoryName": "services-1131"}]}""")

                }                       
            }
            stage('UAT unit test 2') {
                 steps {
                       // snDevOpsStep ()
                        echo "Testing"
                        sh 'mvn -Dtest=com.sndevops.eng.App1Test test'                     
                }
            }     
        }
          post {
              always {
              junit '**/target/surefire-reports/*.xml' 
              }
        }
      
      }

       stage("deploy") {
         stages{
             stage('deploy UAT') {
               steps{
                 //snDevOpsStep ()
                 echo "deploy in UAT"
               }
             }
            stage('deploy PROD') {
                steps{
                 //snDevOpsStep ()
                   echo "deploy in prod"
		//	snDevOpsPackage(name: "sentimentpackage", artifactsPayload: """{"artifacts": [{"name": "sa-web-ui.jar2","repositoryName": "services-1131","version":"${artifactVersion}"}]}""")
                 snDevOpsChange()              
                }
            }
        }
      }
     
    }
     
  }
