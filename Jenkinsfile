pipeline {
    agent any
    tools {
        maven 'Maven 3.3.9'
        jdk 'jdk8'
    }
    stage('Checkout') {
        steps {
            git branch: 'develop',
            credentialsId: 'github-ssh',
            url: 'https://github.com/cloudtraktor/commons-io.git'
        }
        stage('Build and Unit Test'){
            steps {
                sh 'mvn clean compile -Drat.skip=true package'
            }
            post {
                success {
                    junit 'target/surefire-reports/**/*.xml'
                }
            }
        }
        stage('Quality Test') {
            steps {
                sh 'mvn test -Drat.skip=true package'
            }
        }
        stage('Publish Artefact') {
            steps {
            }
        }
        stage('Deploy To Next Stage') {
            steps {
            }
        }
        stage('Declarative: Post Actions') {
            steps {
            }
        }
    }
}
