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
       

                                

      

}
}
