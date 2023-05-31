pipeline {
    agent any
    stages {
        stage('install dep') {
            steps {
               sh 'npm install'
            }
        }
             stage('run tests in jenkins') {
            steps {
                sh 'npm test'
            }
        }
         stage('build the app in container') {
            steps {
                sh ' docker build -t mohamedbedier/app:js . '
            }
        }
         stage('pushing app to repo') {
            steps {
                     withCredentials( [ usernamePassword(credentialsId: 'docker-repo' , passwordVariable: 'PASS' , usernameVariable: 'USER' )] ) {
 
                        sh " docker login -u  $USER -p $PASS "
                        sh ' docker push mohamedbedier/app:js '
                                         
                        }

               sh ' docker push mohamedbedier/app:js '
            }
        }
    

    
    }

}

