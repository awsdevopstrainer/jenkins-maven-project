pipeline {
    agent any
    tools {
        maven "maven3-9-16"
    }
    stages {
        stage('Validate') {
            steps {
                sh 'mvn -f hello-app/pom.xml -B -DskipTests clean validate'
            }
            post {
                success {
                    echo "Validated successfully....."
                }
            }
        }        stage('Build') {
            steps {
                sh 'mvn -f hello-app/pom.xml -B -DskipTests clean compile'
            }
            post {
                success {
                    echo "Compiled successfully....."
                }
            }
        }
        stage('Test') {
            steps {
                sh 'mvn -f hello-app/pom.xml test'
            }
            post {
                always {
                    junit 'hello-app/target/surefire-reports/*.xml'
                }
            }
        }
        stage('Package') {
            steps {
                sh 'mvn -f hello-app/pom.xml -B -DskipTests clean package'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts....."
                    archiveArtifacts artifacts: '**/*.jar'
                }
            }
        }        
    }
}
