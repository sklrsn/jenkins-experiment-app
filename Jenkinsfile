@Library('utils') _

pipeline {
    agent {
        label ''
    }
    stages {
        stage('STG 01') {
            steps {
                script {
                    runShCommand(['command':'date'])
                }
            }
        }
    }
}
