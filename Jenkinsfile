pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        // Checkout the source code from your repository
        // Use the appropriate SCM plugin and configuration for your repository
        // Example: git 'https://github.com/your-repo.git'
        echo 'Git branch Checkout!!!'
      }
    }

    stage('Build Docker Image') {
      steps {
        // Build the Docker image
        script {
          sh '''
            # single sh means single shell, if you use multiple sh 'command 1' sh 'command2' it will run in different shells

            # Change directory to the Docker project
            cd /Users/kiran/devops/docker-example/devops-cicd-testing

            # Print the current working directory
            pwd
            
            #testing
            /Users/kiran/.docker/bin/docker version
            
            #test
            /usr/bin/sw_vers

            # Build the Docker image
            /Users/kiran/.docker/bin/docker build --pull --no-cache -tag demo-app .
            
            /Users/kiran/.docker/bin/docker run -d -p 8909:80 demo-app

        '''
        def exitStatus = sh(script: 'pwd', returnStatus: true) // testing pwd command, if its working or not

        if (exitStatus != 0) {
            error('Shell command failed')
        }
        }
      }
    }

    stage('Push Docker Image') {
      steps {
        // Push the Docker image to a Docker registry
        script {
          sh '''
            # Build the Docker image
              /Users/kiran/.docker/bin/docker push demo-app
          '''
        }
      }
    }

    stage('Deploy to Docker') {
      steps {
        // Deploy the application to the local Docker machine
        script {
          sh '''
            # Build the Docker image
              /Users/kiran/.docker/bin/docker run demo-app
          '''
        }
      }
    }
  }
}

// pipeline {
//     agent any
//     options {
//         timestamps()
//     }
//     // environment {
//     //     AWS_CREDENTIALS = credentials('AWS_secrets_for_s3_upload')
//     // }

//     stages {
//         stage('Build') {
//             steps {
//                 withCredentials([
//                     usernamePassword(credentialsId: 'AWS_secrets_for_s3_upload', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')
//                 ]) {
//                     // script {
//                     //     sh'''
//                     //         /usr/local/bin/aws s3 cp /Users/kiran/devops/docker-example/ s3://sample-dev-deploy-bucket/ --recursive
//                     //     '''
//                     // }
//                 }
//             }
//         }
//         stage('Finalize') {
//             steps {
//                 // Clean up, reporting, notifications, etc.
//                 echo 'Pipeline completed successfully'
//             }
//         }
//     }
// }

// pipeline {
//     agent any
//     stages {
//         stage('Hello') {
//             steps {
//                 echo 'Hello World'
//             }
//         }
//     }
// }