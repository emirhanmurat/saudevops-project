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
        NEXUSIP = 'localhost'
        NEXUSPORT = '8081' 
        NEXUS_GRP_REPO = 'maven-public'
        NEXUS_LOGIN = 'nexuslogin'
    }
    
    stages {
        stage('Build') {
            steps {
                sh 'mvn -s settings.xml -DskipTests install'
            }
        }
    }
}
