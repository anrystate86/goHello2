pipeline {
    agent any
    tools {
        go 'go'
    }
    environment {
        GO111MODULE = 'auto'
        // This can be nexus3 or nexus2
        NEXUS_VERSION = "nexus2"
        // This can be http or https
        NEXUS_PROTOCOL = "http"
        // Where your Nexus is running
        NEXUS_URL = "192.168.100.14:18081"
        // Repository where we will upload the artifact
        NEXUS_REPOSITORY = "golang"
        // Jenkins credential id to authenticate to Nexus OSS
        NEXUS_CREDENTIAL_ID = "nexus3"
    }
    stages {
//        stage("clone code") {
//            steps {
//                script {
//                    // Let's clone the source
//                    git 'https://github.com/danielalejandrohc/cargotracker.git';
//                }
//            }
//        }
        stage('build') {
            steps {
                 sh 'ls -ahl'
                 sh 'pwd'
                 sh 'go build -o helloprogramm.run'
                 sh 'ls -ahl'
            }
        }
        stage("publish to nexus") {
            steps {
                script {
                    // Read POM xml file using 'readMavenPom' step , this step 'readMavenPom' is included in: https://plugins.jenkins.io/pipeline-utility-steps
                    //pom = readMavenPom file: "pom.xml";
                    // Find built artifact under target folder
                    //filesByGlob = findFiles(glob: "target/*.${pom.packaging}");
                    // Print some info from the artifact found
                    //echo "${filesByGlob[0].name} ${filesByGlob[0].path} ${filesByGlob[0].directory} ${filesByGlob[0].length} ${filesByGlob[0].lastModified}"
                    // Extract the path from the File found
                    //artifactPath = filesByGlob[0].path;
                    artifactPath = "helloprogramm.run";
                    // Assign to a boolean response verifying If the artifact name exists
                    artifactExists = fileExists artifactPath;

                    if(artifactExists) {
                        //echo "*** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version}";
                        echo "*** File: ${artifactPath}";
//                        nexusArtifactUploader {
//                        nexusVersion(NEXUS_VERSION)
//                        protocol(NEXUS_PROTOCOL)
//                        nexusUrl(NEXUS_URL)
//                        groupId('test')
//                        version('1')
//                        repository('golang')
//                        credentialsId('nexus3')
//                        artifact {
//                            artifactId(artifactPath)
//                            type('run')
//                            classifier('debug')
//                            file(artifactPath)
 //                       }
                        //artifact {
                        //    artifactId('nexus-artifact-uploader')
                        //    type('hpi')
                        //    classifier('debug')
                        //    file('nexus-artifact-uploader.hpi')
                        //}
//                      }
                        nexusArtifactUploader(
                            nexusVersion: NEXUS_VERSION,
                            protocol: NEXUS_PROTOCOL,
                            nexusUrl: NEXUS_URL,
                            //groupId: pom.groupId,
                            //version: pom.version,
                            repository: NEXUS_REPOSITORY,
                            credentialsId: NEXUS_CREDENTIAL_ID,
                            artifacts: [
                                // Artifact generated such as .jar, .ear and .war files.
                                [//artifactId: pom.artifactId,
                                //classifier: '',
                                file: artifactPath]//,
                                //type: pom.packaging],

                                // Lets upload the pom.xml file for additional information for Transitive dependencies
                                //[artifactId: pom.artifactId,
                                //classifier: '',
                                //file: "pom.xml",
                                //type: "pom"]
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
