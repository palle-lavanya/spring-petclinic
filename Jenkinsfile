pipeline {
    agent {label 'ubuntu'}
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/palle-lavanya/spring-petclinic.git',
                 branch: 'release'
            }
        }
        stage('build') {
            steps {
                sh'./mvnw package'
            } 
        } 
        stage('sonar test'){
            steps{
                withSonarQubeEnv('lavanya') {
                sh './mvnw clean verify sonar:sonar  -Dsonar.organization=palle -Dsonar.projectKey=palle/lavanya'
                }
            }
         }
        stage('publish') {
            steps{
                archiveartifacts artifacts: **/target/*.jar
            }
        }     
      }
    }      
       