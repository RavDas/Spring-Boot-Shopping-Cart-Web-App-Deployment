pipeline {
    agent any

    stages {
        
            stage('Checkout') {
                steps {
                    git branch: 'main', url: 'https://github.com/imcy82/springbootcart.git'
                }
            }
    
            stage('Build') {
                steps {
                    powershell 'mvn package' // Runs the Maven package command to compile the project and package it into a JAR
                }
            }
    
            stage('Test') {
                steps {
                    powershell 'mvn test' // Runs the Maven test command to execute unit tests
                }
            }

            stage('Deploy') {
                steps {
                    bat 'docker build -t shopcart .' // Builds the Docker image

                    bat '''
                        docker run -d ^
                        --name shopcart ^
                        -p 8070:8070 ^
                        shopcart:latest
                    ''' // Runs the Docker container
            }
        }
    }

    post {

        always {
                echo 'Cleaning up workspace'
                deleteDir() // Clean up the workspace after the build
            }
            success {
                echo 'Build succeeded!!!'
                
            }
                failure {
                echo 'Build failed!'
            }
        }
        
}



