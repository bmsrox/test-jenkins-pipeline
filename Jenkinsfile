pipeline {
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
                sh buildProject()
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

def buildProject() {
   if (fileExists('README.md')) {
       return "php -v"
   } else {
       return "echo $USER"
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
