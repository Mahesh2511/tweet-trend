pipeline {
    agent {
        node {
            label 'maven'
        }
    }
environment {
  PATH = "/opt/apache-maven-3.9.6/bin:$PATH"
}    
  stages {
    stage('SonarQube analysis') {
    tools {
        jdk "java21" // the name you have given the JDK installation in Global Tool Configuration
    }
    environment {
      scannerHome = tool 'mahesh01-sonar-scanner'
    }
    steps{
        withSonarQubeEnv('mahesh01-sonar-server') { // If you have configured more than one global server connection, you can specify its name
        sh "${scannerHome}/bin/sonar-scanner"
    }
    }
  }
  stage("Quality Gate"){
    steps {
        script {
           timeout(time: 1, unit: 'HOURS') { // Just in case something goes wrong, pipeline will be killed after a timeout
           def qg = waitForQualityGate() // Reuse taskId previously collected by withSonarQubeEnv
           if (qg.status != 'OK') {
           error "Pipeline aborted due to quality gate failure: ${qg.status}"
           }
           }
       }
    }
 }



    stage('build') {
            steps {
             sh "mvn clean deploy"
            }
    }    
                     
  }
}
