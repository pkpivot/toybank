 pipeline {
     agent any
     stages {
         stage ('build') {
            steps {
                    withMaven ( 
                        maven: 'maven-3-8',
                        mavenLocalRepo: '.repository'
                        ) {
                        sh "mvn package"
                     }
                     withCredentials([sshUserPrivateKey(credentialsId: 'git_automation', keyFileVariable: 'SSH_FILE')]) {
                        sh '''
                        export GIT_SSH_COMMAND="ssh -i $SSH_FILE -o StrictHostKeyChecking=no" git checkout image-build-branch
                        git merge main
                        git push
                        '''
                     }
            }
         }
     }
  }
