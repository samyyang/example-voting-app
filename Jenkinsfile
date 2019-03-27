pipeline {
  agent any
  stages {
    stage('Build result') {
      steps {
        sh 'docker build -t dockersamples/result ./result'
		sh 'docker tag dockersamples/result 192.168.116.130:5000/dockersamples/result'
      }
    } 
    stage('Build vote') {
      steps {
        sh 'docker build -t dockersamples/vote ./vote'
		sh 'docker tag dockersamples/vote 192.168.116.130:5000/dockersamples/vote'
      }
    }
    stage('Build worker') {
      steps {
        sh 'docker build -t dockersamples/worker ./worker'
		sh 'docker tag dockersamples/worker 192.168.116.130:5000/dockersamples/worker'
      }
    }
    stage('Push result image') {
      steps {		
		withDockerRegistry(credentialsId: '115f5357-4b8b-45d5-a033-ebe895b883e9', url: 'http://192.168.116.130:5000') {
		  sh 'docker push dockersamples/result'
        }
      }
    }
    stage('Push vote image') {
      steps {
        withDockerRegistry(credentialsId: '115f5357-4b8b-45d5-a033-ebe895b883e9', url: 'http://192.168.116.130:5000') {
          sh 'docker push dockersamples/vote'
        }
      }
    }
    stage('Push worker image') {
      steps {
        withDockerRegistry(credentialsId: '115f5357-4b8b-45d5-a033-ebe895b883e9', url: 'http://192.168.116.130:5000') {
          sh 'docker push dockersamples/worker'
        }
      }
    }
  }
}
