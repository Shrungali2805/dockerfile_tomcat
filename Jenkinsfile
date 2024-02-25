pipeline {
    agent any
    stages {
        stage('Pull') {
            steps {
                echo "Successful pull from Git"
                git 'https://github.com/deepak-umre/dockerfile_tomcat.git'
            }
        }
        stage('Build') {
            agent {
                label 'docker'
            }
            steps {
                echo "Building with Maven"
                sh 'mvn clean package'
            }
        }
    
        stage('Deploy on Tomcat') {
            agent {
                label 'docker'
            }
            steps {
                script {
                    sh '''cp -r /var/lib/jenkins/workspace/deploy/target/*.war .
                    docker build -t deepakumre/tomcat1 . 
                    docker login 
                    docker push deepakumre/tomcat1'''
                }
            }
        }
        stage('Deploy on Tomcat') {
            agent {
                label 'docker'
            }
            steps {
                script {
                    sh 'kubectl apply -f deployment.yaml'
                }
            }
        }
        stage('Deploy on Tomcat') {
            agent {
                label 'docker'
            }
            steps {
                script {
                    sh '''kubectl get pods -o wide 
                    kubectl get nodes -o wide 
                    kubectl get svc -o wide 
                    ls /var/lib/jenkins/workspace/deploy/target/'''
                }
            }
        }
    }