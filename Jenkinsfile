pipeline {
    agent any

    environment {
        JAVA_HOME = "/usr/lib/jvm/java-17-openjdk"  // adjust if needed
        PATH = "${JAVA_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/mengiejb-collab/springboot.git', branch: 'main'
            }
        }

        stage('Build Fat Jar') {
            steps {
                sh './mvnw clean package -DskipTests' // Maven fat jar
                // For Gradle: sh './gradlew clean build -x test'
            }
        }

        stage('Test') {
            steps {
                sh './mvnw test'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
}
