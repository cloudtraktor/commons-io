pipeline {
    agent any
    tools {
        maven 'Maven 3.3.9'
        jdk 'jdk8'
    }
    stage ('Initialize') {
        steps {
                echo "PATH = ${PATH}"
                echo "M2_HOME = ${M2_HOME}"
        }
    }
    stage('Checkout') {
        steps {
            script {
               git url: 'https://github.com/cloudtraktor/commons-io.git', credentialsId: 'github_credentials'
            }
        }
    }
    stage('Build'){
        agent {
            label "maven"
        }
        steps {
            sh 'mvn clean compile -Drat.skip=true'
        }
    }
    stage('Unit Test') {
        agent {
            label "maven"
        }
        steps {
            sh 'mvn test -Drat.skip=true'
        }
        post {
            success {
                junit 'target/surefire-reports/**/*.xml'
            }
        }
    }
    stage('Publish Artefact') {
        steps {
            // Publish the artefact to Nexus
        }
    }
    stage('Deploy To Develop Stage') {
        steps {
            script {
               env.PIPELINE_NAMESPACE = "develop"
               kubernetesDeploy kubeconfigId: 'docker-desktop', configs: 'k8s/deployment-template.yaml'
            }
        }
    }
    stage('Declarative: Post Actions') {
        steps {
        }
    }
}
