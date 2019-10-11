pipeline {
   agent any
   tools {
      maven 'Maven'
   }
   stages {
       stage("build") {
           steps {
              snDevOpsStep()
               echo "Building" 
                sh 'mvn clean install -DskipTests'
               //sleep 5
           }
       }
       
      stage("test") {
              steps {
                     snDevOpsStep ()
                      echo "Testing"
                      sh 'mvn test'
                }                       
       }
           
      stage("test-1") {
                steps {
                        snDevOpsStep ()
                        echo "Testing"
                       // sh 'mvn -Dtest=com.sndevops.eng.AppTest test'
                }                    
        }

       stage("deploy") {
            steps{
                 snDevOpsStep ()
                 echo "deploy "
                 snDevOpsChange()
            }
                         
       }
     
    }
    post {
              always {
              junit '**/target/surefire-reports/*.xml' 
              }
        }
     
  }
