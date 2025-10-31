pipeline {
    agent node {
        label 'AGENT-1'
    }

    environment {  // just like Docker, k8s laga ney Key:Value pair
        COURSE = 'jenkins'
    }

    options {
        // Timeout counter starts AFTER agent is allocated, Within this time-line not Excuted then it is stopped. 
        timeout(time: 30, unit: 'MINUTES') // this enough normally for microservices
        disableConcurrentBuilds() // Parallel gha Trigger jaraga kunda Prodution lo, we are giving Disable option.
    }

// Build
    stages {
        stage('Build') {
            steps {
                script {
                    sh """
                        echo 'Hello Building..'
                        env   
                    """
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    echo 'Testing..'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    echo 'Deploying....'
                }
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
            // if success, then fine. we will get this message.
        }

        failure { 
            echo ' Hello failure!'
            // In case if it fail, we can trigger the slack, email .. 
        }
    }
}
