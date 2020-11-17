library 'magic-butler-catalogue'
def PROJECT_NAME = 'jenkins-test'
def TRIGGER_STRING = 'test this please'

pipeline {
    triggers {
        issueCommentTrigger('.*test this please.*')
    }
    agent any
    stages {
        stage('Validate PR Source') {
            when {
                expression { env.CHANGE_FORK }
                not {
                    triggeredBy 'issueCommentCause'
                }
            }
            steps {
                echo "An maintainer needs to approve this PR with a comment of '${TRIGGER_STRING}'"
                sh 'false'
            }
        }
        stage('Build') {
            steps {
                echo 'The job is building now O_o!'
            }
        }
        stage('Scanning Image') {
            steps {
                sysdig engineCredentialsId: 'sysdig-secure-api-credentials', name: 'sysdig_secure_images', inlineScanning: true
            }
        }
    }
}
