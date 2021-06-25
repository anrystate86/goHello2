pipeline {
    agent any
    environment {
        GO111MODULE = 'auto'
        // This can be nexus3 or nexus2
        NEXUS_VERSION = "nexus3"
        // This can be http or https
        NEXUS_PROTOCOL = "http"
        // Where your Nexus is running
        //NEXUS_URL = "192.168.100.14:18081"
        NEXUS_URL = Jenkins.getInstance().getComputer('').getHostName()
        // Repository where we will upload the artifact
        NEXUS_REPOSITORY = "golang"
        //NEXUS_REPOSITORY = "nuget-hosted"
        // Jenkins credential id to authenticate to Nexus OSS
        NEXUS_CREDENTIAL_ID = "nexus3"
        ARTIFACT_NAME = "helloprogramm.run"
        ARTIFACT = "helloprogramm"
    }
    stages {
        stage('build') {
            steps {
                 sh 'go build -o $ARTIFACT_NAME' //helloprogramm.run
                 echo $(hostname)
            }
        }
        stage("publish to nexus") {
            steps {
                script {
                    artifactPath = ARTIFACT_NAME;
                    // Assign to a boolean response verifying If the artifact name exists
                    artifactExists = fileExists artifactPath;
                    if(artifactExists) {
                        //echo "*** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version}";
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
