pipeline {
    options { timestamps() }
#    agent { docker { image 'golang:1.16' } }
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
#                // Ensure the desired Go version is installed
#                def root = tool type: 'go', name: 'Go 1.15'

#                // Export environment variables pointing to the directory where Go was installed
#                withEnv(["GOROOT=${root}", "PATH+GO=${root}/bin"]) {
#                    sh 'go version'
#                }
#                sh 'go --version'
#                git clone https://github.com/anrystate86/goHello.git
                 sh 'go build'
            }
        }
    }
}
