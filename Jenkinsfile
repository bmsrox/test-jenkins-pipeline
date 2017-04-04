node {
    try {
        stage("Checkout") {
           checkout scm
        }
        stage("test") {
           echo "Testing"
        }
        stage("deploy") {
            echo "Deploy"
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

    def enviroment = getEnvironment()
    status = status ?: 'SUCCESS'

    if (status == 'SUCCESS') {
        message = "Uma nova versão do software esta liberada no ambiente de '${enviroment}'"
    } else {
        message = "Ocorreu algo errado no pipeline! Favor verificar."
    }

    sendEmail(message, status)
}

def sendEmail(String message, String statusName) {
    mail (
        to: "bms_sp@hotmail.com",
        cc: "bmsrox@gmail.com",
        subject: "${statusName}: Job '${env.JOB_NAME}' [${env.BUILD_NUMBER}]",
        mimeType: 'text/html',
        body: message
    );
}
