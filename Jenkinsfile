pipeline {
    agent any
    environment {
        GO111MODULE = 'auto'
        // This can be nexus3 or nexus2
        NEXUS_VERSION = "nexus3"
        // This can be http or https
        NEXUS_PROTOCOL = "http"
        // Where your Nexus is running
        NEXUS_URL = "nexus:8081"
        // Repository where we will upload the artifact
        NEXUS_REPOSITORY = "golang"
        // Jenkins credential id to authenticate to Nexus OSS
        NEXUS_CREDENTIAL_ID = "nexus3"
        ARTIFACT_NAME = "helloprogramm2.run"
        ARTIFACT = "helloprogramm2"
    }
    stages {
        stage('build') {
            steps {
                 sh 'go build -o $ARTIFACT_NAME'; 
            }
        }
        stage("publish to nexus") {
            steps {
                script {
                    artifactPath = ARTIFACT_NAME;
                    // Assign to a boolean response verifying If the artifact name exists
                    artifactExists = fileExists artifactPath;
                    if(artifactExists) {
                        echo "*** File: ${artifactPath}";
                        nexusArtifactUploader(
                            nexusVersion: NEXUS_VERSION,
                            protocol: NEXUS_PROTOCOL,
                            nexusUrl: NEXUS_URL,
                            groupId: 'group',
                            version: '1',
                            repository: NEXUS_REPOSITORY,
                            credentialsId: NEXUS_CREDENTIAL_ID,
                            artifacts:  [
                                [artifactId: ARTIFACT,
                                classifier: '1',
                                file: ARTIFACT_NAME,
                                type: 'run'],
                            ]
                        );

                    } else {
                        error "*** File: ${artifactPath}, could not be found";
                    }
                }
            }
        }
    }

}
