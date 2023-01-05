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

        stage('STG 02') {
            steps {
                script {
                    try {
                        runMakeCommand(['command':'build', 'path':''])
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
            println 'always'
        }

        failure {
            println 'failure'
        }

        aborted {
            println 'aborted'
        }
    }
}
