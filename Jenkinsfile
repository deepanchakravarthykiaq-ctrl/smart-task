
pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'ap-south-1'

        S3_BUCKET = 'smart-task-management-frontend-2026-unique'

        CLOUDFRONT_DISTRIBUTION_ID = 'E9F0IEYOTKN4P'
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo 'Checking out GitHub source code'
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                dir('frontend') {
                    sh 'npm ci'
                }
            }
        }

        stage('Build React Frontend') {
            steps {
                dir('frontend') {
                    sh 'npm run build'
                }
            }
        }

        stage('Verify Build') {
            steps {
                script {
                    if (!fileExists('frontend/dist/index.html')) {
                        error 'Frontend build failed: index.html not found!'
                    }

                    echo 'Frontend build verified successfully'
                }
            }
        }

        stage('Deploy to AWS S3') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-credentials'
                ]]) {
                    sh '''
                        echo "Checking AWS credentials..."
                        aws sts get-caller-identity

                        echo "Deploying frontend to S3..."

                        aws s3 sync frontend/dist/ s3://${S3_BUCKET}/ --delete

                        echo "S3 deployment completed successfully!"
                    '''
                }
            }
        }

        stage('Invalidate CloudFront') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-credentials'
                ]]) {
                    sh '''
                        echo "Invalidating CloudFront cache..."

                        aws cloudfront create-invalidation \
                            --distribution-id ${CLOUDFRONT_DISTRIBUTION_ID} \
                            --paths "/*"

                        echo "CloudFront invalidation submitted!"
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'SUCCESS: Application deployed to AWS!'
            echo 'S3 and CloudFront deployment completed.'
            echo 'Website: https://d3vdgb83ez6afn.cloudfront.net'
        }

        failure {
            echo 'FAILED: Check Jenkins Console Output.'
        }

        always {
            echo 'Jenkins CI/CD Pipeline execution completed.'
        }
    }
}
