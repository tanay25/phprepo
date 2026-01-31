pipeline {
    agent any

    stages {

        stage('Clone Repo') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/tanay25/phprepo.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    if [ -f composer.json ]; then
                        composer install --no-dev --optimize-autoloader
                    else
                        echo "No composer.json found"
                    fi
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    if [ -f vendor/bin/phpunit ]; then
                        vendor/bin/phpunit
                    else
                        echo "PHPUnit not found, skipping tests"
                    fi
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    rsync -av --delete \
                    --exclude='.git' \
                    --exclude='Jenkinsfile' \
                    --exclude='node_modules' \
                    ./ /var/www/html/
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Deployment Successful"
        }
        failure {
            echo "❌ Pipeline Failed"
        }
    }
}
