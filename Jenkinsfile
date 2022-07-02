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
                sh 'ssh deploy@ip-10-0-1-208.eu-west-1.compute.internal "cd forum; \
                git pull origin master; \
                composer install --optimize--autoloader --no-dev; \
                php aritsan migrate --force; \
                php artisan chache:clear; \
                php artisan config:cache;"'
            }
        }
    }
}
