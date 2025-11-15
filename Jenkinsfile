pipeline {
    agent any

    stages {

        stage('Build with Maven') {
            steps {
                sh './mvnw clean package'
            }
        }

        stage('Upload JAR to Nexus') {
            steps {
                sh '''
                JAR_FILE=target/spring-boot-complete-0.0.1.jar

                curl -v -u admin:12f07269-659c-4218-9c10-e4f5c0eb31a1 \
                --upload-file $JAR_FILE \
                "http://localhost:8081/repository/maven-releases/com/example/springboot/spring-boot-complete/0.0.1/spring-boot-complete-0.0.1.jar"
                '''
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
}

