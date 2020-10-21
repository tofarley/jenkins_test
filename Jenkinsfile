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
                allOf {
                    expression { env.CHANGE_FORK }
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
    }
}
