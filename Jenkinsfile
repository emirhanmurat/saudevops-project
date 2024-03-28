pipeline {
    agent any
    tools {
        maven "MAVEN3"
        jdk "OracleJDK8"
    }
    
    environment {
        SNAP_REPO = 'maven-snapshots'
		NEXUS_USER = 'admin'
		NEXUS_PASS = '[F7s0W@dImFRt1rN`AT,'
		RELEASE_REPO = 'maven-releases'
		CENTRAL_REPO = 'maven-central'
		NEXUSIP = '192.168.1.138'
		NEXUSPORT = '8081'
		NEXUS_GRP_REPO = 'maven-public'
        NEXUS_LOGIN = 'nexuslogin'
    }

       stages {
        stage('Build'){
            steps {
                sh 'mvn -s settings.xml -DskipTests install'
            }
            post {
                success {
                    echo "Now Archiving."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }

        stage('Test'){
            steps {
                sh 'mvn -s settings.xml test'
            }

        }

        stage('Checkstyle Analysis'){
            steps {
                sh 'mvn -s settings.xml checkstyle:checkstyle'
            }
        }
    }
}