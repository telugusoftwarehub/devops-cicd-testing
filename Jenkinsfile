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
          docker.build("my-app:${env.BUILD_NUMBER}")
        }
      }
    }

    stage('Push Docker Image') {
      steps {
        // Push the Docker image to a Docker registry
        script {
          docker.withRegistry('https://your-docker-registry', 'your-docker-credentials') {
            docker.image("my-app:${env.BUILD_NUMBER}").push()
          }
        }
      }
    }

    stage('Deploy to Docker') {
      steps {
        // Deploy the application to the local Docker machine
        script {
          docker.withServer('your-docker-machine-url') {
            docker.image("my-app:${env.BUILD_NUMBER}").run("-p 8080:80")
          }
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