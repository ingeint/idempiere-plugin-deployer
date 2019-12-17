pipeline {
    agent {
        docker { image 'docker:19' }
    }
    environment {
        PROJECT_NAME = 'idempiere-deployer'
        TAG_NAME = "${GIT_BRANCH == 'master' ? 'latest' : GIT_BRANCH}"
        REGISTRY_PASS = credentials('ingeint-registry-pass')
    }
    stages {
        stage('Publish to Registry') {
            steps {
                sh 'docker login $REGISTRY_REPOSITORY -u $REGISTRY_USER -p $REGISTRY_PASS'
                sh 'docker build -t $REGISTRY_REPOSITORY/$PROJECT_NAME:$TAG_NAME .'
                sh 'docker push $REGISTRY_REPOSITORY/$PROJECT_NAME:$TAG_NAME'
            }
        }
    }
}