pipeline {
    agent any
        tools {
            maven 'Maven'
        }
    stages{
        stage('Git checkout'){
            steps{
                checkout(
                    [
                        $class: 'GitSCM', 
                        branches: [[name: '*/master']
                    ], 
                    extensions: [], 
                    userRemoteConfigs: [
                        [
                            url: 'https://github.com/sandeepmchary/java_home.git'
                        ]
                                        ]
                    ])
            }
        }
        stage ('Build'){
            steps{
                sh "mvn clean package"
            }
        }
        stage ('Uploading Artifacts to Nexus'){
            steps{
                script{
                def mavenPom = readMavenPom file: 'pom.xml'
                nexusArtifactUploader artifacts: [
                    [
                        artifactId: 'simple-app', 
                        classifier: '', 
                        file: "target/simple-app-${mavenPom.version}.war", 
                        type: 'war'
                        ]
                    ],
                     credentialsId: 'Nexus_pass', 
                     groupId: 'in.javahome', 
                     nexusUrl: '172.31.26.46:8081', 
                     nexusVersion: 'nexus3', 
                     protocol: 'http', 
                     repository: 'simpleapp-release', 
                     version: "${mavenPom.version}"
                }
            }
        }
        
    }
}