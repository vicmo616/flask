pipeline {
  agent {
    node {
      label 'docker'
    }

  }
  stages {
    stage('Git') {
      steps {
        git(url: 'https://github.com/vicmo616/flask', branch: 'main')
      }
    }

    stage('Build') {
      steps {
        sh 'docker build -t vicmo616/flask-app .'
      }
    }

    stage('Docker Login') {
      steps {
        sh 'docker login -u vicmo616 -p dckr_pat_pMC63bEF2z-CeAlm2HGUCogy5zo'
      }
    }

    stage('Docker Push') {
      steps {
        sh 'docker push vicmo616/flask-app'
      }
    }

  }
}