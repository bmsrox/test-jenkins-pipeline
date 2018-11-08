def userInput = true
def didTimeout = false
try {
    timeout(time: 15, unit: 'SECONDS') { // change to a convenient timeout for you
        userInput = input(
        id: 'Proceed1', message: 'Was this successful?', parameters: [
        [$class: 'BooleanParameterDefinition', defaultValue: true, description: '', name: 'Please confirm you agree with this']
        ])
    }
} catch(err) { // timeout reached or input false
    def user = err.getCauses()[0].getUser()
    if('SYSTEM' == user.toString()) { // SYSTEM means timeout.
        didTimeout = true
    } else {
        userInput = false
        echo "Aborted by: [${user}]"
    }
}

node {
    if (didTimeout) {
        // do something on timeout
        echo "no input was received before timeout"
    } else if (userInput == true) {
        // do something
        echo "this was successful"
    } else {
        // do something else
        echo "this was not successful"
        currentBuild.result = 'FAILURE'
    } 
}

/*pipeline {
    agent any
    parameters {
        string(name: 'EMAIL', defaultValue: 'bruno.santos@ftd.com.br, bms_sp@hotmail.com')
    }
    stages {
        stage('Example') {
            steps {
                echo params.EMAIL
                echo getEnvironment()
            }
        }
        stage('Build') {
            steps {
                echo "Project built"
            }
        }
        
        stage ('Test') {
            steps {
                sh "export ENV_TEST=${getEnvironment()}"
                print showCommit()
            }
        }
    }
    post {
        success {
            mail (
                to: params.EMAIL,
                subject: "SUCCESS: Job '${env.JOB_NAME}' [${env.BUILD_NUMBER}]",
                mimeType: 'text/html',
                body: "A new software version has been released!"
            );
        }
        failure {
            mail (
                to: params.EMAIL,
                subject: "FAILURE: Job '${env.JOB_NAME}' [${env.BUILD_NUMBER}]",
                mimeType: 'text/html',
                body: "Something went wrong!"
            );
        }
    }
}

def showCommit() {
gitCommit = sh(returnStdout: true, script: 'git rev-parse HEAD').trim()
// short SHA, possibly better for chat notifications, etc.
shortCommit = gitCommit.take(6)
    return shortCommit
}

def getEnvironment() {
    def branch = "${env.BRANCH_NAME}"
    if (branch == "master") {
        return "Production"
    } else if (branch == "staging") {
        return "Staging"
    } else {
        return "Development"
    }
}
/*node {
    try {
           
        properties([parameters([string(name: 'ENV', defaultValue: getEnvironment())])])
        
        stage("Checkout") {
           checkout scm
        }
        stage("test") {
            echo "${params.ENV}"
        }
        stage("deploy") {
            echo "Deploy to ${params.ENV}"
        }
    } catch (e) {
        currentBuild.result = "FAILED"
        throw e
    } finally {
        notifyStatus(currentBuild.result)
    }
}

def getEnvironment() {
    def branch = "${env.BRANCH_NAME}"
    if (branch == "master") {
        return "Production"
    } else if (branch == "staging") {
        return "Staging"
    } else {
        return "Development"
    }
}

def notifyStatus(String status) {
    status = status ?: 'SUCCESS'

    if (status == 'SUCCESS') {
        message = "A new software version has been released in '${environment}'"
    } else {
        message = "Something went wrong on project build! Please check it. '${env.BUILD_URL}'"
    }

    sendEmail(message, status)
}

def sendEmail(String message, String statusName) {
    mail (
        to: "bmsrox@gmail.com, bms_sp@hotmail.com",
        subject: "${statusName}: Job '${env.JOB_NAME}' [${env.BUILD_NUMBER}]",
        mimeType: 'text/html',
        body: message
    );
}
*/
