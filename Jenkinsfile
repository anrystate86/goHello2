pipeline {
    agent any
    tools {
        go 'go'
    }
    environment {
        GO111MODULE = 'auto'
    }
    stages {
        stage('build') {
            steps {
                 sh 'ls -ahl'
                 sh 'pwd'
                 sh 'go build'
            }
        }
    }
}
