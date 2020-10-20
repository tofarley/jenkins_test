library 'magic-butler-catalogue'
def PROJECT_NAME = 'jenkins-test'
def TRIGGER_STRING = 'test this please'

pipeline {
    triggers {
        issueCommentTrigger('.*test this please.*')
    }
    agent any
    stages {
        // stage('Validate') {
        //     when { expression { env.CHANGE_FORK } }
        //     steps {
        //         script {
        //             if (!env.GITHUB_COMMENT || !(env.GITHUB_COMMENT.contains('test this please')) ) {
        //                 sh """
        //                 echo "You're on a fork. Get outta here!"
        //                 exit 1
        //             """
        //             } else {
        //                 sh """
        //                 echo $GITHUB_COMMENT
        //                 exit 0
        //             """
        //             }
        //         }
        //     }
        // }
        stage('Test') {
            when { expression { !env.CHANGE_FORK || (env.GITHUB_COMMENT && env.GITHUB_COMMENT =~ env.TRIGGER_STRING) } }
            environment {
                CREDS_FILE = credentials('pipeline-e2e-creds')
                LOGDNA_HOST = "logs.use.stage.logdna.net"
            }
            steps {
                script {
                    if (env.GITHUB_COMMENT && env.GITHUB_COMMENT =~ env.TRIGGER_STRING) {
                        sh """
                            echo "Runs when not on a fork, or when the comment happens"
                    """
                    } else if (!env.CHANGE_FORK) {
                        sh """
                            echo "We are on a fork, but no comment has happened. quit!"
                            exit 1
                        """
                    }
                    def creds = readJSON file: CREDS_FILE
                    // Assumes the pipeline-e2e-creds format remains the same. Chase
                    // refer to the e2e tests's README's authorization docs for the
                    // current structure
                    LOGDNA_INGESTION_KEY = creds["packet-stage"]["account"]["ingestionkey"]
                }
            }
        }
        stage('Build') {
            steps {
                script {
                        sh """
                        echo "The job is building now O_o!"
                    """
                }
            }
        }
    }
}
