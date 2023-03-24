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
                withSonarQubeEnv('sonar') {
                sh './mvnw clean package sonar:sonar -Dsonar.organization=palle -Dsonar.projectKey=palle/lavanya'
                }
            }
         }
        stage('publish') {
            steps{
                archiveartifacts artifacts: '**/target/*.jar'
            }
        }
        stage('copying jar file') {
            steps{
                sh 'sudo cp  /home/ubuntu/laav/workspace/name1_develop/target/spring-petclinic-3.0.0-SNAPSHOT.jar /tmp'
            }
        }
        stage('deploy') {
            steps{
                sh 'ansible-playbook -i hosts ansible.yaml'
            }
        }
                   
      }
    }      
       
