pipeline {
   agent any

    stages {
        stage('START') {
            steps {
                slackSend channel: 'build-jenkins',
                color: 'good',
                message: "Started $JOB_NAME $BUILD_NUMBER",
                tokenCredentialId: '74ccf0ef-9dc6-4a55-93c9-640cd2e28803'
            }
        }
        stage('Git checkout') {
            steps {
                slackSend channel: 'build-jenkins',
                color: 'good',
                message: 'Pulling from Git',
                tokenCredentialId: '74ccf0ef-9dc6-4a55-93c9-640cd2e28803'
                
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '**']],
                    doGenerateSubmoduleConfigurations: false,
                    extensions: [],
                    submoduleCfg: [],
                    userRemoteConfigs: [[
                        credentialsId: 'f649fe87-53cb-43e2-b095-633a3f4d8fa7',
                        url: 'https://github.com/Apig-Sharbo/guacamole-client.git'
                    ]]
                ])        
            }
        }
        stage ('Compile Stage') {

            steps {
                withMaven(jdk: 'java-8', maven: 'maven-3.6.3') {
                    sh 'mvn package'
                }
            }
        }
        /*stage ('Testing Stage') {

            steps {
                withMaven(jdk: 'java-8', maven: 'maven-3.6.3') {
                    sh 'mvn test'
                }
            }
        }*/
        stage('END') {
            steps {
                slackSend channel: 'build-jenkins',
                color: 'good',
                message: 'Build Success',
                tokenCredentialId: '74ccf0ef-9dc6-4a55-93c9-640cd2e28803'
            }
        }
        /*
        
        
        stage('Upload to Nexus') {
            steps {
                nexusArtifactUploader 
                artifacts: [
                    [
                        artifactId: 'guacamole-client',
                        classifier: '',
                        file: 'guacamole/target/guacamole-1.2.0.war',
                        type: 'war'
                    ],
                    [
                        artifactId: 'guacamole-client',
                        classifier: '',
                        file: 'guacamole/pom.xml',
                        type: 'pom'
                    ]
                ], 
                credentialsId: '63b50af5-a815-49da-a096-8830e9d5698b',
                groupId: 'guacamole-client-group',
                nexusUrl: 'localhost:8081',
                nexusVersion: 'nexus3',
                protocol: 'http',
                repository: 'maven-releases',
                version: '3.$BUILD_NUMBER'
            }
        }
        
        */
    }
}
