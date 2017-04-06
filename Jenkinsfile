pipeline {
    agent any
    properties([
       parameters([
            string(name: 'REQUESTER_MAIL', defaultValue: 'rafael.araujo@ftd.com.br'),
            string(name: 'DEVS_MAIL', defaultValue: 'bruno.santos@ftd.com.br, marcos.tavares@ftd.com.br'),
            string(name: 'ENV', defaultValue: getEnvironment()),
       ])
    ])
    stages {
        stage('Get Envs') {
            steps {
                echo ${params.REQUESTER_MAIL}
                echo ${params.DEVS_MAIL}
                echo ${params.ENV}
            }
        }
    }
    post {
        success {
            echo 'I succeeeded!'
        }
        failure {
            echo 'I failed :('
        }
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
