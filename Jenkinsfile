node {
    try {
        stage("Checkout") {
           checkout scm
        }
        stage("test") {
           echo "Test"
        }
        stage("deploy") {
            echo "Deploy"
        }
    } catch (e) {
        throw e
    } finally {
        notifyStatus()
    }
}

def notifyStatus() {
emailext (
      to: $DEFAULT_RECIPIENTS,
      subject: "SUCCESS: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
      body: """<p>SUCCESS: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>"""
    )
}
