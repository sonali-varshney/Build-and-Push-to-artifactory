pipeline {
    agent any
    tools{
        maven 'maven-3.8.6'
    }

    stages {
        stage('Clone the repository') {
            steps {
               git credentialsId: 'Github_username_password', url: 'https://github.com/techworldwithmurali/Build-and-Push-to-artifactory.git'
            }
        }
        
    
        stage('Build the code') {
            steps {
            sh 'mvn clean deploy'
                 }
    }
    
    stage('Push to Nexus artifactory') {
            steps {
            nexusPublisher nexusInstanceId: 'Nexus-3', nexusRepositoryId: 'maven-snapshots', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: '/var/lib/jenkins/workspace/Build-and-Push-to-artifactory/target/web-application.war']], mavenCoordinate: [artifactId: 'web-application', groupId: 'com.techworldwithmurali', packaging: 'war', version: '1.0-SNAPSHOT']]]
                 }
    }
}
}
