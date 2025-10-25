pipeline {
    agent {
        label 'terraform-slave'
    }
    parameters {
        choice(
            name: 'ACTION',
            choices: 'validate\ninit\nplan\napply\ndestroy'
        )
    }

    environment {
        GOOGLE_APPLICATION_CREDENTIALS = "${WORKSPACE}/sa-key.json"
    }
    stages {
        stage ('Setup GCE Auth') {
            steps {
                withCredentials([file(credentialsId: 'gcp-service-account-key', variable: 'SA_KEY')]) {
                    // some block
                    sh '''
                        cp $SA_KEY $GOOGLE_APPLICATION_CREDENTIALS
                    '''
                }
            }
        }

        // Initialize terraform
        stage('init') {
            steps {
                echo "Initialising the terraform"
                sh "terraform init"
            }
        }

        // Plan 
        stage ('plan') {
            when {
                expression {
                    params.ACTION == 'plan'
                }
            }
            steps {
                echo "Executing the plan for terraform"
                sh "terraform plan"
            }
        }

        // Apply 
        stage ('apply'){
            when {
                expression {
                    params.ACTION == 'apply'
                }
            }
            steps {
                echo "Applying terraform infra"
                sh "terraform apply --auto-approve"
            }
        }

        // Destroy 
        stage ('destroy') {
            when {
                expression {
                    params.ACTION == 'destroy'
                }
            }
            steps {
                echo "Destroying the terraform infra"
                // terraform destroy
            }
        }
    }
}