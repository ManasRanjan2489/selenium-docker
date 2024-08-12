pipeline{

    agent any

    stages{

        stage('Build Jar'){
            steps{
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Build Image'){
            steps{
                bat 'docker build -t=manas2489/selenium:latest .'
            }
        }

        stage('Push Image'){
            environment{
                DOCKER_HUB = credentials('dockerhub-creds')
            }
            steps{
                bat 'docker login -u %DOCKER_HUB_USR% -p %DOCKER_HUB_PSW%'
//                 bat 'echo ${DOCKER_HUB_PSW} | docker login -u ${DOCKER_HUB_USR} --password-stdin'
                bat 'docker push manas2489/selenium:latest'
                bat "docker tag manas2489/selenium:latest manas2489/selenium:${env.BUILD_NUMBER}"
                bat "docker push manas2489/selenium:${env.BUILD_NUMBER}"
            }
        }

    }

    post {
        always {
            bat 'docker logout'
        }
    }

}