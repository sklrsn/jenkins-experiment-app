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
                        buildAlert(['medium':'CONSOLE',
                                    'status':'FAILURE',
                                    'jobname': env.JOB_NAME,
                                    'buildnumber':env.BUILD_NUMBER,
                                    'buildUrl': env.BUILD_URL,
                                    'displayUrl':env.RUN_DISPLAY_URL,
                                    'console': currentBuild.rawBuild.getLog(100).toString(),
                                    'changes': getChangelogAsString(),
                                    'stages': [ 'UNIT_TESTS', 'SMOKE_TESTS', 'BUILD_BINARIES' ]
                                    ])
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

def getChangelogAsString() {
    def changes = getChanges()
    def changeString = ''
    changes.each { entry ->
        changeString += " - $entry.key - $entry.value\n"
    }
    if (!changeString) {
        changeString = ' - No new changes'
    }
    return changeString
}

def getChanges() {
    def changes = [:]
    def changeLogSets = currentBuild.changeSets

    for (int i = 0; i < changeLogSets.size(); i++) {
        def entries = changeLogSets[i].items
        for (int j = 0; j < entries.length; j++) {
            def entry = entries[j]
            truncated_msg = entry.msg.take(50)
            if (changes.containsKey(entry.author)) {
                changes[entry.author].add(truncated_msg)
            } else {
                changes[entry.author] = [truncated_msg]
            }
        }
    }
    return changes
}
