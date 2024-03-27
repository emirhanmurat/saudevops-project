pipeline {
    agent any
    tools {
        maven "MAVEN3"
        jdk "OracleJDK8"
    }
    
    environment {
        SNAP_REPO = 'devops-snapshot'
        NEXUS_USER = 'admin'
        NEXUS_PASS = '[F7s0W@dImFRt1rN`AT,'
        RELEASE_REPO = 'devops-release'
        CENTRAL_REPO = 'devops-maven-central'
        NEXUSIP = 'localhost'
        NEXUSPORT = '8081' 
        NEXUS_GRP_REPO = 'devops-maven-group'
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
