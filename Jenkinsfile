pipeline {
    agent any

    // tools{
    //     maven 'maven3.9'
       
    // }
    
    stages {
        stage('git Checkout') {
            steps {
                git branch:'anmolmalik711-patch-1', url: 'https://github.com/Soul-of-steel/Multi_App_Platform.git'
            }
        }
        stage('build'){
            steps{
                sh ' ./mvnw clean install ' // mvn clean install
				
				
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('Mysonarqube') {
                        sh ' ./mvnw sonar:sonar'  // mvn sonar:sonar
                        
                }
            }
        }
        stage('Docker Image Build & Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'Dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    script {
                         sh 'docker build -t soulofsteel/oct-batch:v1.0.0 .'
                         sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
                         sh 'docker images'
          
                    }
               }
           }
        }             
    }
}
