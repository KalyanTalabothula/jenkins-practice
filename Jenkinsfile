pipeline {
// PRE-Build Session
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

    parameters { // 1st-time parameters telidu dhaniki jenkins, 2nd time excute inappudu chupistumdhi. okkasari excute ite ghani telidu. Parameters Use chestunnaru ani. 
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }

// Build Session
    stages {
        stage('Build') {
            steps {
                script {
                    sh """
                        echo 'Hello Building..'
                        sleep 10
                        env   
                        echo "Hello ${params.PERSON}"  
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
            input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
            }

            steps {
                script {
                    echo "Hello, ${PERSON}, nice to meet you."
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


/* 🗂️ What is “workspace”?

Every Jenkins job gets its own workspace folder on the server,
where Jenkins:

Downloads your code (from Git)
Builds it
Runs tests
Stores temporary files

Example path:

/var/lib/jenkins/workspace/my-project/

👉 It deletes all files and folders inside that workspace after the build finishes.

So next time Jenkins runs that job, it starts fresh — with a clean empty folder.


🧠 Why we use it (purpose):

🧹 Clean up old files → remove leftover code, logs, build artifacts
🚫 Avoid conflicts → old files might cause errors in next build
🔁 Ensure fresh build every time → Jenkins pulls new code again 

deleteDir() = clean the workspace after build → so next build starts with a fresh, empty folder. */