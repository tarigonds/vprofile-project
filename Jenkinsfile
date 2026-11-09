pipeline {
    agent any
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
