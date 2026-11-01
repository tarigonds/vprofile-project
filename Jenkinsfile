pipeline {
    agent any
    stages{

        stage('Fetch Code') {
            steps {
                git branch: 'paac', url: 'https://github.com/tarigonds/vprofile-project.git'
            }
        }
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
