pipeline {
    agent any
    tools{
        maven 'MAVEN3'
        jdk "JAVA11"
    }
    stages{
       stage('BUILD'){
            steps {
                sh 'mvn clean install -DskipTests'
            }
            
        }

        stage('UNIT TEST'){
            steps {
                sh 'mvn test'
            }
        }
    }
}
