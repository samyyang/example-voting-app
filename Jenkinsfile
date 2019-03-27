pipeline {
  agent any
  
  parameters{
      string(name:'harbor_url',defaultValue:'192.168.116.130:5000',description:'harvor_url')
  }
  
  stages {
    stage('Build result') {
      steps {
        sh 'docker build -t dockersamples/result ./result'
		sh 'docker tag dockersamples/result "${params.harbor_url}"/dockersamples/result'
      }
    } 
    stage('Build vote') {
      steps {
        sh 'docker build -t dockersamples/vote ./vote'
		sh 'docker tag dockersamples/vote "${params.harbor_url}"/dockersamples/vote'
      }
    }
    stage('Build worker') {
      steps {
        sh 'docker build -t dockersamples/worker ./worker'
		sh 'docker tag dockersamples/worker "${params.harbor_url}"/dockersamples/worker'
      }
    }
    stage('Push result image') {
      steps {		
		withDockerRegistry(credentialsId: '115f5357-4b8b-45d5-a033-ebe895b883e9', url: 'http://192.168.116.130:5000') {
		  sh 'docker push "${params.harbor_url}"/dockersamples/result'
        }
      }
    }
    stage('Push vote image') {
      steps {
        withDockerRegistry(credentialsId: '115f5357-4b8b-45d5-a033-ebe895b883e9', url: 'http://192.168.116.130:5000') {
          sh 'docker push "${params.harbor_url}"/dockersamples/vote'
        }
      }
    }
    stage('Push worker image') {
      steps {
        withDockerRegistry(credentialsId: '115f5357-4b8b-45d5-a033-ebe895b883e9', url: 'http://192.168.116.130:5000') {
          sh 'docker push "${params.harbor_url}"/dockersamples/worker'
        }
      }
    }
  }
}
