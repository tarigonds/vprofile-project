pipeline{
    agent any
    tools{
        jdk 'JAVA11'
        maven 'MAVEN3'
    }
    environment{
        SNAP_REPO = 'vprofile-snapshot'
        RELEASE_REPO = 'vprofile-release'
        CENTRAL_REPO = 'vprofile-central'
        NEXUS_GRP_REPO = 'vpro-maven-group'
        NEXUSIP = '172.31.1.57'
        NEXUSPORT = '8081'
        NEXUS_USER = 'admin'
        NEXUS_PASS = 'Admin@123'
        NEXUS_LOGIN = 'nexuslogin'
    }
    stages{
        stage('Build'){
            steps{
                sh 'mvn clean package'
                sh 'mvn -s settings.xml -DskipTests install'
            }
            post{
                success{
                    echo "Now Archiving"
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage('UNIT TEST'){
            steps{
                sh 'mvn test'
            }
        }
        stage('INTEGRATION TEST'){
            steps{
                sh 'mvn verify -DskipUnitTests'
            }
        }
        stage('Checkstyle Analysis'){
            steps{
                sh 'mvn checkstyle:checkstyle'
            }
        }
        stage('sonar Analysis'){
            environment{
                scannerHome = tool "${SONARSCANNER}"

            }
            steps{
                withSonarQubeEnv("${SONARSERVER}"){
                    sh '''''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=vprofile \
                   -Dsonar.projectName=vprofile-repo \
                   -Dsonar.projectVersion=2.0 \
                   -Dsonar.sources=src/ \
                   -Dsonar.java.binaries=target/test-classes/com/visualpathit/account/controllerTest/ \
                   -Dsonar.junit.reportsPath=target/surefire-reports/ \
                   -Dsonar.jacoco.reportsPath=target/jacoco.exec \
                   -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml'''
                }
            }
        }
        stage('Quality gate'){
            steps{
                timeout(time: 10, unit: 'MINUTES'){
                    waitForQualityGate abortPipeline: true
                }
            }
        }
        stage('UploadArtifacts'){
            steps{
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol:"http",
                    nexusUrl: "${NEXUSIP}:${NEXUSPORT}",
                    groupId: 'siva',
                    version: "${env.BUILD_ID}-${env.BUILD_TIMESTAMP}",
                    repository: "${RELEASE_REPO}",
                    credentialsId: "${NEXUS_LOGIN}",
                    artifacts:[
                        [artifactId: 'vproapp',
                        classifier: '',
                        file: 'target/vprofile-v2.war',
                        type: 'war']
                    ]
                )
            }
        }
    }
}
