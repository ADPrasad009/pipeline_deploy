pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'devopsdeepdive2', url: 'https://github.com/devopsdeepdive/maven-web-project.git']]])
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
     /*  stage('Test') {
            steps {
                bat 'mvn test'
        }
    } */
         stage('Deploy') {
            steps {
                bat 'mvn install tomcat7:deploy'
        }
    }
     stage('Notification') {
            steps {
                slackSend channel: '#pipeline-jobs', color: 'good', iconEmoji: ':with:grin:', message: 'Build is succesful and deployed', tokenCredentialId: 'slack'
        }
    }
}
}
