@Library('utils') _

pipeline {
    agent {
        label ''
    }
    stages {
        stage('STG 01') {
            steps {
                script {
                    try {
                        runShCommand(['command':'date'])
                    }catch (Exception ex) {
                        println ex
                    }
                }
            }
        }
    }
    post {
        success {
            println 'success'
        }

        always {
            println 'failure'
        }

        failure {
            println 'failure'
        }

        aborted {
            println 'abort'
        }
    }
}
