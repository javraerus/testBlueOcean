pipeline {
    agent any
echo "hola"
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                withDockerContainer("php:7-fpm") {
                     sh "php -v"
                 }
                
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
