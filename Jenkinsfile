pipeline {
    agent { label 'ubuntuu' } // Ensure it runs on the Ubuntu slave

    environment {
        JAVA_HOME = "/usr/lib/jvm/java-17-openjdk-amd64"
        PATH = "$JAVA_HOME/bin:$PATH"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/muthu512/spring-boot-hello-world.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy Application') {
            steps {
                sh 'nohup java -jar target/*.jar > output.log 2>&1 &'
            }
        }
    }

    post {
        success {
            echo "Deployment successful!"
        }
        failure {
            echo "Deployment failed!"
        }
    }
}
