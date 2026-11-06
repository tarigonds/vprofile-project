pipeline{
    agent any
    tools{
        jdk "JAVA21"
        maven "MAVEN3"
    }
     environment {
        SNAP_REPO ='vprofile-snapshot'
        RELEASE_REPO ='vprofile-release'
        CENTRAL_REPO ='vprofile-central'
        NEXUS_GRP_REPO ='vpro-maven-group'
        NEXUSIP ='172.31.12.196'
        NEXUSPORT ='8081'
        NEXUS_USER ='admin'
        NEXUS_PASS ='Admin@123'
        NEXUS_LOGIN ='nexuslogin'
        SONARSERVER ='sonarserver'
        SONARSCANNER ='sonarscanner'
    }
    stages{
        stage('Build'){
            steps{
                sh 'mvn -s settings.xml -DskipTests install'
            }
            post{
                success{
                    cho "Now Archiving"
                    archiveArtifacts artifacts: '**/*.war'

                }
            }
        }
    }
}
