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
                echo 'Tarefa Paralela 01'
            },
            'config route': {
                echo 'Tarefa Paralela 02'
            }
        )
    }
    stage('Docker Build') {
        sh 'docker build -t murilopaixao2/laravel:$BUILD_NUMBER .'
    }
    
    stage('Docker Ship') {
        sh 'docker push murilopaixao2/laravel:$BUILD_NUMBER'
    }
}
