pipeline {
    agent any
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/palle-lavanya/spring-petclinic.git',
                 branch: 'develop'
            }
        }
        stage('build') {
            steps {
                sh'./mvnw package'
            } 
        } 
        stage('sonar test'){
            steps{
                withSonarQubeEnv('sonar') {
                sh './mvnw clean verify sonar:sonar  -Dsonar.organization=palle -Dsonar.projectKey=palle/lavanya'
                }
            }
         }
      }
    }      
        
