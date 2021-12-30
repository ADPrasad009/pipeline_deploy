pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'git', url: 'https://github.com/ADPrasad009/pipeline_deploy.git']]])
            }
        }
         stage('Build') {
            steps {
                bat 'mvn validate'
        }
    }
        stage('package') {
            steps {
                bat 'mvn clean package'
        }
    }
       stage('Test') {
            steps {
                bat 'mvn test'
        }
    } 
         stage('Deploy') {
            steps {
                bat 'mvn install tomcat7:deploy'
        }
    }
     stage('Notification') {
            steps {
                slackSend channel: '#jenkins_pipeline.', color: 'good', message: 'Build is succesful', tokenCredentialId: 'slacknotification'
    }
}
}
