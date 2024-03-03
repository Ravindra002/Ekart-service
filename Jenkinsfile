pipeline {
    agent any
    tool name: 'maven3', type: 'maven'
    tool name: 'jdk17', type: 'jdk'
    environment {
        SCANNER_HOME = tools 'sonar-scanner'
    }
    stages {
        // stage ('Install tools') {
        //         script {
        //             // Specify the tool installations
        //             def jdkTool = tool name: 'jdk17', type: 'jdk'
        //             def mavenTool = tool name: 'maven3', type: 'maven'

        //             // Set environment variables for the tools
        //             env.JAVA_HOME = "${jdkTool}"
        //             env.PATH = "${jdkTool}/bin:${mavenTool}/bin:${env.PATH}"
        //         }
        // }
        stage ('Checkout from SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/Ravindra002/Ekart-service.git'
            }
        }
        stage ('Compile') {
            steps {
                sh 'mvn compile'
            }
        }
        stage ('Unit test') {
            steps {
                sh 'mvn test' //-DskipTests=true
            }
        }
        stage ('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube-Server') {
                    sh '''
                        $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=EKART -Dsonar.projectName=EKART \
                        -Dsonar.java.binaries=.
                    '''
                }
            }
        }
        
    }
}
