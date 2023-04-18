pipeline {
    environment {
        registry = 'vicmo616/flask-app'
        registryCredentials = 'docker'
        cluster_name = 'skillstorm'
        namespace = 'vicmo616'
    }
  agent {
    node {
      label 'docker'
    }

  }
  stages {
    stage('Git') {
      steps {
        git(url: 'https://github.com/vicmo616/flasky', branch: 'main')
      }
    }
stage('Build Stage') {
    steps {
        script {
            dockerImage = docker.build(registry)
        }
      }
    }
stage('Deploy Stage') {
    steps {
        script {
           docker.withRegistry('', registryCredentials) {
                dockerImage.push()
            }
          }
        }
      }
stage('Kubernetes'){
  steps{
     withCredentials([aws(accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'AWS_SECRET_ACCESS_KEY')]) {
      script{
        try{
          sh "kubectl create namespace ${namespace}"
        }catch (Exception e) {
          echo "Exception handled"
        }
      }
      sh "kubectl apply -f deployment.yaml -n ${namespace}"
      sh "kubectl -n ${namespace} rollout restart deployment flaskcontainer"
    }
  }
}
    }
}
