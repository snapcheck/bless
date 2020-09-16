pipeline {
  agent any
  stages {
    stage('Setup') {
      steps {
        sh 'cd bless'
        sh 'aws s3 cp s3://blessca-keys/bless-ca- lambda_configs/bless-ca-'
      }
    }

    stage('Package') {
        steps {
            sh 'make develop'
        }
    }
    
    stage('Compile') {
      steps {
        sh 'make lambda-deps'
             
      }
    }
  
    stage('publish') {
      steps {
        sh 'make publish'
             
      }
    }

    stage('Deploy') {
        steps {
            sh 'aws lambda create-function \
            --function-name bless \
            --runtime python3.7 \
            --zip-file fileb://publish/bless_lambda.zip \
            --handler bless_lambda_user.lambda_handler_user \
            --role arn:aws:iam::383800542185:role/bless-access \
            --timeout 10'
        }
    }
  }
}