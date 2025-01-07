pipeline {
    agent any
    options {
        // Timeout counter starts AFTER agent is allocated
        timeout(time: 20, unit: 'SECONDS')
    }
    stages {
        stage('Example') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Setup') { // Install any dependencies you need to perform testing
            steps {
                script {
                  sh """
                  hostname
                  """
                }
            }
        }
    }
}
