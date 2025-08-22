pipeline {
    agent any

    environment {
        PROJECT_NAME = 'MyProject'
        BUILD_DIR = 'build'
        ARCHIVE_DIR = 'archive'
    }

    options {
        // Set a timeout of 1 hour for this pipeline
        timeout(time: 1, unit: 'HOURS') 
    }

    stages {
        stage('Initialize') {
            steps {
                echo 'Initializing pipeline...'
                /*sh 'mkdir -p $BUILD_DIR'
                sh 'mkdir -p $ARCHIVE_DIR'*/
            }
        }

        stage('Checkout SCM') {
            steps {
                echo 'Checking out source code from SCM...'
                checkout scm
            }
        }

        stage('Setup Environment') {
            steps {
                echo 'Setting up environment...'
                /*sh 'python3 -m venv venv'
                sh './venv/bin/pip install -r requirements.txt'*/
            }
        }

        stage('Static Code Analysis') {
            steps {
                echo 'Running static code analysis...'
               // sh './venv/bin/flake8 .'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
               // sh './venv/bin/python setup.py build'
            }
        }

        stage('Unit Tests') {
            steps {
                echo 'Running unit tests...'
               // sh './venv/bin/pytest tests/unit --junitxml=unit-test-report.xml'
            }
        }

        stage('Integration Tests') {
            steps {
                echo 'Running integration tests...'
                //sh './venv/bin/pytest tests/integration --junitxml=integration-test-report.xml'
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging the application...'
                //sh 'tar -czvf $ARCHIVE_DIR/$PROJECT_NAME.tar.gz -C $BUILD_DIR .'
            }
        }

        stage('Archive Artifacts') {
            steps {
                echo 'Archiving build artifacts...'
               // archiveArtifacts artifacts: '$ARCHIVE_DIR/*.tar.gz', onlyIfSuccessful: true
            }
        }

        stage('Deploy to Test Environment') {
            steps {
                echo 'Deploying to test environment...'
               // sh 'scp $ARCHIVE_DIR/$PROJECT_NAME.tar.gz user@test-server:/deployments/'
                //sh 'ssh user@test-server "cd /deployments && tar -xzvf $PROJECT_NAME.tar.gz && ./deploy.sh"'
            }
        }

        stage('Automated Acceptance Tests') {
            steps {
                echo 'Running automated acceptance tests...'
               // sh './venv/bin/pytest tests/acceptance --junitxml=acceptance-test-report.xml'
            }
        }

        stage('Deploy to Production') {
            when {
                branch 'main'
            }
            steps {
                input message: 'Deploy to production?', ok: 'Deploy'
                echo 'Deploying to production...'
               // sh 'scp $ARCHIVE_DIR/$PROJECT_NAME.tar.gz user@prod-server:/deployments/'
               // sh 'ssh user@prod-server "cd /deployments && tar -xzvf $PROJECT_NAME.tar.gz && ./deploy.sh"'
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
