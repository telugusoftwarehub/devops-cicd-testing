pipeline {
    agent any
    options {
        timestamps()
    }
    // environment {
    //     AWS_CREDENTIALS = credentials('AWS_secrets_for_s3_upload')
    // }

    stages {
        stage('Build') {
            steps {
                withCredentials([
                    usernamePassword(credentialsId: 'AWS_secrets_for_s3_upload', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')
                ]) {
                    script {
                        sh'''
                            /usr/local/bin/aws s3 cp /Users/kiran/devops/docker-example/ s3://sample-dev-deploy-bucket/ --recursive
                        '''
                    }
                }
            }
        }
        stage('Finalize') {
            steps {
                // Clean up, reporting, notifications, etc.
                echo 'Pipeline completed successfully'
            }
        }
    }
}