pipeline {
    agent any
    environment {
        //be sure to replace "willbla" with your own Docker Hub username
        DOCKER_IMAGE_NAME = "spring/wunderit"
    }
    tools {
        maven 'Maven 3.6.1'
        jdk 'jdk8'
    }
    stages {

        stage ('Chekout') {
            steps {
                 echo 'checkout stage'
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
        stage ('Docker build') {
             steps {
                  echo 'mvn clean package docker:build'
                 // ignore spotify dockerfile-maven  
                 //  sh 'mvn clean package docker:build'
             }
        }
        stage ('Release') {
              steps {
                   echo 'mvn clean package docker:build'
                  // ignore plugin maven-releas
                  // sh 'mvn release:clean release:prepare'
                    }
        }
        stage('DeployToProduction') {
            when {
                branch 'master'
            }
            steps {
                input 'Deploy to Production?'
                milestone(1)
                kubernetesDeploy(
                    kubeconfigId: 'kubeconfig',
                    configs: 'deploy.yml',
                    enableConfigSubstitution: true
                )
            }
        }
    }
}
