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
    stages {

        // Initialize terraform
        stage('init') {
            steps {
                echo "Initialising the terraform"
                // terraform init
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
                // terraform plan 
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
                //terraform apply 
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