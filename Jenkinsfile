pipeline{
    agent any
    
    environment{
        IMAGE_NAME="piyush5621/calculator-app"
    }

    stages{
        stage('clone'){
            steps{
                git branch: 'main',
                url: 'https://github.com/Piyush5621/calculator-app.git'
            }
        }

        stage('Maven Build'){
            steps{
                script{
                    sh 'mvn clean package'
                }
            }
        }

        stage('Docker Build'){
            steps{
                script{
                    docker.build("${IMAGE_NAME}:latest")
                }
            }
        }

        stage('Docker Push'){
            steps{
                script{
                    docker.withRegistry(
                        'https://index.docker.io/v1/',
                        'dockerhub-calculator'
                    ){
                        docker.image("${IMAGE_NAME}:latest").push()
                    }
                }
            }
        }
        
    }
}
