pipeline {
    options { timeout() }
    agent any
    tools {
        go 'go'
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
