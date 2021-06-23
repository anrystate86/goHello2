pipeline {
    options { timeout() }
    agent any
    tools {
        go 'go-1.15'
    }
    environment {
        GO111MODULE = 'on'
    }
    stages {
        stage('build') {
            steps {
                 sh 'go build'
            }
        }
    }
}
