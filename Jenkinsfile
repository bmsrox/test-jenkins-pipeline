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


def notifyStatus(String status) {

    status = status ?: 'SUCCESS'

    if (status == 'SUCCESS') {
        message = "Uma nova versão do software esta liberada no ambiente de '${BRANCH_NAME}'"
    } else {
        message = "Ocorreu algo errado no pipeline! Favor verificar."
    }

    sendEmail(message, status)
}

def sendEmail(String message, String statusName) {
    mail (
        to: "bms_sp@hotmail.com",
        cc: "bmsrox@gmail.com",
        subject: "${statusName}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
        mimeType: 'text/html',
        body: message
    );
}
