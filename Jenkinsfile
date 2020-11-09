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
        stage('Render') {
        steps {
            echo "Rendering k8s artifacts"
            withCredentials([
            string(
                credentialsId: 'sysdig-agent-access-key',
                variable: 'SYSDIG_AGENT_ACCESS_KEY')
            ]) {
            sh 'echo $SYSDIG_AGENT_ACCESS_KEY'
            sh 'echo $SYSDIG_AGENT_ACCESS_KEY > /tmp/key.tmp'
            sh 'cat /tmp/key.tmp'
            sh 'echo $GCLOUD_SERVICE_KEY_B64'
            sh 'SYSDIG_AGENT_ACCESS_KEY=$(printf $SYSDIG_AGENT_ACCESS_KEY | base64)'
            sh 'SYSDIG_AGENT_ACCESS_KEY=$(printf $SYSDIG_AGENT_ACCESS_KEY)'
            sh 'env'
            sh 'printenv'
            sh 'ls -lah /tmp/workspace/answerbook_logdna-workers_PR-181'
            sh 'ls ${JENKINS_HOME}'
            }
        }
        }
    }
}
