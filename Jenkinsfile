pipeline{
    agent any
    tools{
        jdk "JAVA11"
        maven "MAVEN3"
    }
    environment{
        SNAP_REPO ='vprofile-snapshot'
        RELEASE_REPO ='vprofile-relase'
        CENTRAL_REPO ='vprofile-central'
        NEXUS_GRP_REPO ='vpro-maven-group'
        NEXUSIP ='172.31.6.63'
        NEXUSPORT ='8081'
        NEXUS_USER ='admin'
        NEXUS_PASS ='Admin@123'
        NEXUS_LOGIN ='nexuslogin'
    }
    stages{
        stage('Build'){
            steps{
                sh 'mvn -s settings.xml -DskipTests install'
            }
        }
    }
}
