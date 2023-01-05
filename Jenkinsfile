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

        stage('STG 03') {
            steps {
                script {
                    try {
                        runShCommand(['command':'env'])
                    }catch (Exception ex) {
                        println ex
                    }
                }
            }
        }

        stage('STG 04') {
            steps {
                script {
                    try {
                        buildAlert(['medium':'CONSOLE', status:'SUCCESS', 'buildnumber':env.BUILD_NUMBER, 'buildurl': env.RUN_DISPLAY_URL])
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
