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
            //when { expression { !env.CHANGE_FORK || (env.GITHUB_COMMENT && env.GITHUB_COMMENT =~ env.TRIGGER_STRING) } }
            steps {
                script {
                    if (env.CHANGE_FORK) {
                        if (env.GITHUB_COMMENT && env.GITHUB_COMMENT =~ env.TRIGGER_STRING) {
                            sh """
                                echo "We are on a fork, and a comment has occured!"
                        """
                        } else {
                                sh """
                                echo "We are on a fork, but no comment has happened. quit!"
                                exit 1
                        """
                        }
                    }
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
