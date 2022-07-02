pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'composer install'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh './vendor/bin/phpunit'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production'
                sh 'ssh deploy@ip-10-0-1-49.eu-west-1.compute.internal "cd /sites/forum; \
                git pull origin master; \
                composer install --optimize-autoloader --no-dev; \
                php artisan migrate --force; \
                php artisan cache:clear; \
                php artisan route:cache; \
                php artisan config:cache;"'
            }
        }
    }
}
