def buildNumber = Jenkins.instance.getItem('awsbean-pipeline').lastSuccessfulBuild.number
def COLOR_MAP = [
    'SUCCESS': 'good', 
    'FAILURE': 'danger',
]
pipeline {
    agent any
    tools {
        maven "MAVEN3"
        jdk "TemurinJDK11"
    }
    
    environment {
        SNAP_REPO = 'maven-snapshots'
		NEXUS_USER = 'admin'
		NEXUS_PASS = '[F7s0W@dImFRt1rN`AT,'
		RELEASE_REPO = 'maven-releases'
		CENTRAL_REPO = 'maven-central'
		NEXUSIP = '192.168.1.128'
		NEXUSPORT = '8081'
		NEXUS_GRP_REPO = 'maven-public'
        NEXUS_LOGIN = 'nexuslogin'
        SONARSERVER = 'sonarserver'
        SONARSCANNER = 'sonarscanner'
        ARTIFACT_NAME = "vprofile-v${buildNumber}.war"
        AWS_S3_BUCKET = 'saudevops-bean'
        AWS_EB_APP_NAME = 'production-saudevops'
        AWS_EB_ENVIRONMENT = 'Production-saudevops-env'
        AWS_EB_APP_VERSION = "${buildNumber}"


    }

       stages {
        stage('Deploy to Stage Bean'){
          steps {
            withAWS(credentials: 'awsbeancred', region: 'eu-north-1') {
               sh 'aws elasticbeanstalk update-environment --application-name $AWS_EB_APP_NAME --environment-name $AWS_EB_ENVIRONMENT --version-label $AWS_EB_APP_VERSION'
            }
          }
        }
    }
    post {
        always {
            echo 'Slack Notifications.'
            slackSend channel: '#bitirme-projesi',
                color: COLOR_MAP[currentBuild.currentResult],
                message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} \n More info at: ${env.BUILD_URL}"
        }
    }
}