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
                sh 'mvn validate'
        }
    }
        stage('package') {
            steps {
                sh 'mvn clean package'
        }
    }
       stage('Test') {
            steps {
                sh 'mvn test'
        }
    } 
         stage('Deploy') {
            steps {
                sh 'mvn install tomcat7:deploy'
        }
    }
     stage('Notification') {
            steps {
                slackSend channel: '#jenkins_pipeline.', color: 'good', message: 'Build is succesful', tokenCredentialId: 'slacknotification'
    }
}
}

