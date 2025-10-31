pipeline {
    agent node {
        label 'AGENT-1'
    }
// Build
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
// POST session will be mentioned after the Build Session
    post { 
        always { 
            echo 'I will always say Hello again!'
            deleteDir() // For without clashing the other pipelines we are deleting.
            // In case we neeed to Debug anything, then comment this deleteDir, then check. 
        }

        success { 
            echo ' Hello success!'
        }

        failure { 
            echo ' Hello failure!'
        }
    }
}
