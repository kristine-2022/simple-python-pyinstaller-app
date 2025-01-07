pipeline {
    agent none
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
            agent { node { label '10.15.0.25' } }
            steps {
                script {
                  sh """
                  hostname
                  """
                }
            }
        }
        stage('Build') {
            agent {     
                node {
                    label '10.15.0.25'
                    customWorkspace '/home/fn/jenkins/otherpath'
                }
            } 
            steps {
                //This sh step runs the Python command to compile your application and
                //its calc library into byte code files, which are placed into the sources workspace directory
                sh 'python -m py_compile sources/add2vals.py sources/calc.py'
                //This stash step saves the Python source code and compiled byte code files from the sources
                //workspace directory for use in later stages.
                stash(name: 'compiled-results', includes: 'sources/*.py*')
            }
        }
    }
}
