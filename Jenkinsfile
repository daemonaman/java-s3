pipeline {
    agent any

    environment {
        // Define your AWS credentials stored in Jenkins
        AWS_ACCESS_KEY_ID = credentials('aws-access-key-id') // Add Jenkins credentials ID here
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access-key') // Add Jenkins credentials ID here
        S3_BUCKET = 'your-s3-bucket-name' // S3 bucket name
        AWS_REGION = 'your-region' // Example: us-east-1
    }
    stages {
        stage('Pull code from git') {
            steps {
                git branch: 'dev', credentialsID:'jenkins',url:'git repository url'
     }
}
        stage('Build') {
            steps {
                Maven build 
            }
        }

        stage('Archive Artifact to S3') {
            steps {
                // Upload the file to S3 using AWS CLI
                sh """
                    aws configure set aws_access_key_id ${AWS_ACCESS_KEY_ID}
                    aws configure set aws_secret_access_key ${AWS_SECRET_ACCESS_KEY}
                    aws configure set region ${AWS_REGION}

                    # Replace "artifact-file-name" with your actual file name
                    aws s3 cp target/artifact-file-name s3://${S3_BUCKET}/
                """
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            // You can add any cleanup steps if needed
        }
    }
}
