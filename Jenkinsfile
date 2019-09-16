pipeline {
   agent any
   tools {
      maven 'Maven'
   }
   stages {
       stage("build") {
           steps {
              snDevOpsStep '8d92e433dbf7bf40963c5c55dc961995'
               echo "Building" 
                sh 'mvn clean install -DskipTests'
               sleep 5
           }
       }
       
       stage("test") {
           steps {
               snDevOpsStep '0992e433dbf7bf40963c5c55dc961995'
               echo "Testing"
               sh 'mvn test -Dpublish'
               sleep 3
           }
          post {
                always {
                    junit '**/target/surefire-reports/*.xml' 
                }
          }
        }

       stage("deploy") {
           steps {
               snDevOpsStep '0192e433dbf7bf40963c5c55dc961996'
               snDevOpsChange()
               echo "Deploying"
               // release process
               // release process
               sleep 7
           }
       }
   }
}
