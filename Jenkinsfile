pipeline {
    agent {
        node {
            label 'maven'
        }
    }
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage('git clone') {
            steps {
             git branch: 'main', url: 'https://github.com/Mahesh2511/tweet-trend.git'
            }
        }    
                     
    }
}
