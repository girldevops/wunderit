pipeline {
    agent any
    tools {
        maven 'Maven 3.6.1'
        jdk 'jdk8'
    }
    stages {

        stage ('Chekout') {
            steps {
               // git branch: 'master', credentialsId: '3b03b4d0-fcde-4df0-8b0b-5d58d10649c9', url: 'https://github.com/girldevops/wunderit.git'
            }
        }
        stage ('Check') {
            steps {
                echo 'Check PMD violations'
                sh 'mvn pmd:check '
            }
        }
        stage ('Test') {
            steps {
                echo 'lunch junit test '
                sh 'mvn test '
            }
        }
        stage ('Deploy') {
            steps {
                echo 'download dependencies to nexus '
                sh 'mvn clean deploy'
            }
        }
    }
}
