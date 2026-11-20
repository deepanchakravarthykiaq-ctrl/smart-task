
pipeline {
    agent any

    environment {
        AWS_REGION = 'ap-south-1'
        S3_BUCKET = 'smart-task-management-frontend-2026-unique'
        CLOUDFRONT_ID = 'E9F0IEYOTKN4P'
        AWS_CREDENTIALS = 'aws-credentials'
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
                    if (fileExists('frontend/build')) {
                        env.BUILD_DIR = 'frontend/build'
                    } else if (fileExists('frontend/dist')) {
                        env.BUILD_DIR = 'frontend/dist'
                    } else {
                        error 'React build output not found!'
                    }
                }

                echo "Build directory: ${env.BUILD_DIR}"
            }
        }

        stage('Deploy to AWS S3') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'aws-credentials',
                        usernameVariable: 'AWS_ACCESS_KEY_ID',
                        passwordVariable: 'AWS_SECRET_ACCESS_KEY'
                    )
                ]) {
                    sh '''
                        export AWS_DEFAULT_REGION=$AWS_REGION

                        aws s3 sync "$BUILD_DIR/" \
                        "s3://$S3_BUCKET/" \
                        --delete
                    '''
                }
            }
        }

        stage('Invalidate CloudFront') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'aws-credentials',
                        usernameVariable: 'AWS_ACCESS_KEY_ID',
                        passwordVariable: 'AWS_SECRET_ACCESS_KEY'
                    )
                ]) {
                    sh '''
                        aws cloudfront create-invalidation \
                        --distribution-id "$CLOUDFRONT_ID" \
                        --paths "/*"
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'SUCCESS: React frontend deployed!'
            echo 'Website: https://d3vdgb83ez6afn.cloudfront.net'
        }

        failure {
            echo 'FAILED: Check Jenkins console output.'
        }
    }
}
