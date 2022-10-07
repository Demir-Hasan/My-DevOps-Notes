```Jenkinsfile
pipeline {
    agent any
    stages {
        stage('Requirements') {
            steps {
                echo 'Getting Requirements....'
            }
        }
        stage('Build') {
            steps {
                echo 'Building....'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..1'
                echo 'Testing..2'
                echo 'Testing..3'
            }
        }
        stage('Report') {
            steps {
                echo 'Reporting....'
            }
        }
    }
}
```



```Jenkinsfile
pipeline {
    agent any
    parameters {
      choice choices: ['DEVELOPMENT', 'STAGING', 'PRODUCTION'], 
         description: 'Choose the environment for this deployment.', 
         name: 'ENVIRONMENT'
      
      password defaultValue: '123ABC', 
         description: 'Enter the API key to use for this deployment.', 
         name: 'API_KEY'
      
      text defaultValue: 'This is the change log.', 
         description: 'Enter the components that were changed in this deployment.', 
         name: 'CHANGELOG'
    }    
    stages {
        stage('Test') {
            steps {
                echo "This step tests the compiled project"
            }
        }
        stage('Deploy') {
            when {
              expression { params.ENVIRONMENT == "PRODUCTION" }
            }            
            steps {
                echo "This step deploys the project"
            }
        }        
        stage('Report') {
            steps {
                echo "This stage generates a report"
                sh "printf \"${params.CHANGELOG}\" > ${params.ENVIRONMENT}.txt"
                archiveArtifacts allowEmptyArchive: true, 
                    artifacts: '*.txt', 
                    fingerprint: true, 
                    followSymlinks: false, 
                    onlyIfSuccessful: true
            }
        }
    }
}
```


```
pipeline {
    agent any
    parameters {
        choice(name: 'ENVIRONMENT',
            choices: ['DEVELOPMENT' , 'STAGING', 'PRODUCTION'],
            description: 'Choose the environment for this deployment')
    }

    stages {
        stage ('Build') {
            steps {
                echo "Building..."
            }
        }
        stage ('Deploy to non-production environments') {
            when {
                // Only deploy if the environment is NOT production
                expression { params.ENVIRONMENT != 'PRODUCTION' }
            }
            steps {
                echo "Deploying to ${params.ENVIRONMENT}"
            }
        }
        stage ('Deploy to production environment') {
            when {
                expression { params.ENVIRONMENT == 'PRODUCTION' }
            }
            steps {
                input message: 'Confirm deployment to production...', ok: 'Deploy'
                echo "Deploying to ${params.ENVIRONMENT}"
            }
        }
    }
}
```
