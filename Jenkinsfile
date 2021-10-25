
pipeline {
    agent any
    environment {
        ADMIN_TOKEN = credentials('artifactory-admin-token')
        VERSION = readMavenPom().getVersion()
    }
    stages {
        stage('Compile') {
            steps {
                echo 'Compiling...'
                sh "mvn compile"
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                sh "mvn test"
            }
        }
        stage('Package') {
            steps {
                echo 'Packaging...'
                sh "mvn package -Dmaven.test.skip"
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
                sh 'curl -u jenkins:$ADMIN_TOKEN -X PUT "http://artifactory:8081/artifactory/maven-artifactory/junit/junit-$VERSION.jar" -T target/junit-$VERSION.jar'
            }
        }
    }
}
