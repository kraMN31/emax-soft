pipeline {
    agent any
    tools{
        maven 'M2_HOME'
    }
    environment {
        registry = '740955001227.dkr.ecr.us-east-1.amazonaws.com/emax-geoloc-ecr'
        registryCredential = 'jenkins-ecr'
        dockerimage = ''
    }
    stages {
        stage('Checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/kraMN31/emax-soft-repo.git'
            }
        }
        stage('Code Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        // Building Docker images
        stage('Building image') {
            steps{
                script {
                    dockerImage = docker.build registry + ":latest"
                }
            }
        }
        // Uploading Docker images into AWS ECR
        stage('Pushing to ECR') {
            steps{
                script {
<<<<<<< HEAD
                    sh 'docker tag emax_ecr_repo:latest 740955001227.dkr.ecr.us-east-1.amazonaws.com/emax-geoloc-ecr:latest'
                    sh 'aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 740955001227.dkr.ecr.us-east-1.amazonaws.com'
=======
                    sh 'docker tag emax-geoloc-ecr:latest 740955001227.dkr.ecr.us-east-1.amazonaws.com/emax-geoloc-ecr:latest'
                    sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 740955001227.dkr.ecr.us-east-1.amazonaws.com'
>>>>>>> a50c7dda7bb88944b1b23ea7ba8ea227ba0114b1
                    sh 'docker push 740955001227.dkr.ecr.us-east-1.amazonaws.com/emax-geoloc-ecr:latest'
                }
            }
        }
    }
}