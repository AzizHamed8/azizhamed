pipeline {
    agent any

    tools {
        maven "M2_HOME"
    }

    environment {
        SONAR_TOKEN = 'ton_token_sonarqube'  // Remplace par ton token
    }

    stages {
        stage('GIT') {
            steps {
                git branch: 'master', url: 'https://github.com/AzizHamed8/azizhamed.git'
            }
        }

        stage('COMPILE') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('MVN Sonarqube') {
            steps {
                sh 'mvn sonar:sonar -Dsonar.login=squ_c9263050f3e9762c15fe61f601fdc2a28ca3632a -Dmaven.test.skip=true'

            }
        }
    }
}
