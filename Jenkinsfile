node('php'){
    stage('Clean'){
        deleteDir()
        sh 'ls -la'
    }
    
    stage('Fetch') {
        checkout scm
    }
    
    stage('Build'){
        sh 'composer install --no-scripts --prefer-dist --no-dev --ignore-platform-reqs'
    }
    
    stage('config') {
        parallel(
            'config cache': {
                echo 'Tarefa Paralela'
            },
            'config route': {
                sh 'php artisan'
            }
        )
    }
    stage('Docker Build') {
        sh 'docker build -t murilopaixao2/api:$BUILD_NUMBER .'
    }
    
    stage('Docker Ship') {
        sh 'docker push murilopaixao2/api:$BUILD_NUMBER'
    }
}
