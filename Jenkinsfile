pipeline {
    agent {
        node {
            label "maven"
        }
    }

    tools {
        jdk "java11"
    }

environment {

    PATH = "/opt/apache-maven-3.9.6/bin:$PATH"
    scannerHome = tool 'sonar'
}

    stages {
        stage('Cloning the code from git') {
          steps {
            git branch: 'main', url: 'https://github.com/sriuday19/tweet-trend-new.git'
          }
        }

        stage('Build code') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('SonarQube Analysis') {
            tools {
                jdk "java17"
            }
            steps {
                withSonarQubeEnv('sonar-server') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
    }
}