pipeline {
  agent any
    stages {
        stage('Pull') {
             steps{
                script{
                    checkout([$class: 'GitSCM', branches: [[name: '*/master']],
                        userRemoteConfigs: [[
                            credentialsId: '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',
                            url: 'https://github.com/sarra96zr/MyApp.git']]])
                }
            }
        }
        stage('Install') {
             steps{
                script{
                    sh "sudo npm install"
                }
            }
        }   

         stage('Build'){
	      steps{
                     script{
                          sh "ansible-playbook Ansible/build.yml -i Ansible/inventory/host.yml"
			   }
		   }
	     }
         stage('Docker'){
            steps{
                script{
                    sh "ansible-playbook Ansible/docker.yml -i Ansible/inventory/host.yml "
                }
            }
        }
       
        stage('docker_registry') {
           steps{
               script {
                   sh "ansible-playbook Ansible/docker-registry.yml -i Ansible/inventory/host.yml "
               }
           }
         }
             stage ('Email Notification') {
steps {
mail bcc: '', body: 'your pipeline is building', cc: '', from: '', replyTo: '', subject: 'Build', to: 'zribisarahzribi@gmail.com'
}
}     

      

}
}
