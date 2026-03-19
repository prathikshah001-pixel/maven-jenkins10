pipeline {
    agent any
    tools {
        maven 'Maven3'
        jdk 'JAVA11'
    }
    stages {
        stage('Download Code') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/prathikshah001-pixel/maven-jenkins10.git']])
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Generate Artifacts') {
            steps {
                archiveArtifacts artifacts: '**/*.war', followSymlinks: false
            }
        }
        stage('trigger Deploy pipeline') {
            steps {
                build wait: false, job: 'deploy-pipeline'                
            }
        }
    }
}
