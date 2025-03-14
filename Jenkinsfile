pipeline {
    agent any

    tools {
        jdk 'JAVA_HOME'
        maven "M2_HOME"
    }

    environment {
        SONAR_TOKEN = 'ton_token_sonarqube'  // Remplace par ton token
         IMAGE_NAME = "azizhamed/test"
        IMAGE_VERSION = "1.0.1"
    }

    stages {
        stage('GIT') {
            steps {
                git branch: 'master', url: 'https://github.com/AzizHamed8/azizhamed.git'
            }
        }

        // stage('COMPILE') {
        //     steps {
        //         sh 'mvn clean compile'
        //     }
        // }
   


        // stage('MVN Sonarqube') {
        //     steps {
        //         sh 'mvn sonar:sonar -Dsonar.login=squ_c9263050f3e9762c15fe61f601fdc2a28ca3632a -Dmaven.test.skip=true'

        //     }
        // }


             stage('Compile') {
            steps {
                sh 'mvn clean compile'
            }
        }
   stage('MVN Nexus') {
    steps {
        script {
            sh 'mvn deploy -Dmaven.test.skip=true'
        }
    }
}

        //      stage('Building image') {
        //     steps {
        //         sh 'docker build -t azizhamed/timesheet-devops:1.0.0 .'
        //     }
        // }
        // stage('Deploy Image') {
        //             steps {
        //                 sh 'docker build -t azizhamed/timesheet-devops:1.0.0 .'
        //             }
        //         }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'sudo docker build -t ${IMAGE_NAME}:${IMAGE_VERSION} .'
                }
            }
        }

        stage('Login to DockerHub') {
            steps {
                script {
              withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh 'echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin'

                    }
                }
            }
        }
      stage('Push Docker Image') {
            steps {
                script {
                    sh 'docker push ${IMAGE_NAME}:${IMAGE_VERSION}'
                }
            }
        }
        stage('Verify docker-compose.yml') {
    steps {
        script {
            sh 'ls -la'  // This will list all files in the workspace to check if docker-compose.yml is present
        }
    }
}

             stage('Run Docker Compose') {
            steps {
                script {
                    // Run Docker Compose in detached mode
                    sh 'docker compose -f docker-compose.yml up -d'
                }
            }
        }

    }
}
