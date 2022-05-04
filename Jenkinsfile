pipeline {

environment { 

    registry = "apoorvvns/jenkins-test" 

    registryCredential = '92450add-9fc3-483e-bf8b-68c396379a18' 

   dockerImage = '' 

}

agent any 

stages { 

    stage('Cloning our Git') { 

        steps { 

            git 'https://github.com/apoorvpandey-ap/Docker_1/' 

        }

    } 

    stage('Building our image') { 

        steps { 

            script { 

                dockerImage = docker.build registry + ":$BUILD_NUMBER"

            }

        } 

    }

    stage('Deploy our image') { 

        steps { 

            script { 

                docker.withRegistry( '', registryCredential ) {

                    dockerImage.push() 

                }

            } 

        }

    } 

    stage('Cleaning up') { 

        steps { 

            sh "docker rmi $registry:$BUILD_NUMBER" 

        }

    } 

}
}
