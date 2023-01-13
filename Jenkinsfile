pipeline {
    agent any
    stages {
        stage('step 1 : Git') {
            steps {
                echo "GitHub clone step"
                git branch: "MED",
                url: "https://github.com/aymenESP/achatDEVOPS.git"
            }
        }
        stage('step 2 :  Maven') {
            steps {
                sh 'mvn clean compile -DskipTests'
            }
        }
        /*
        stage('MVN CLEAN') {

            steps {

                sh 'mvn -version'

                sh 'mvn clean'

            }

        }
*/
      /*  stage('MVN TEST (Mockito)') {

           steps {

              sh 'mvn test'

            }

        }*/

        stage('step 3 : SonarQube') {
            steps {
                sh   "mvn sonar:sonar -Dsonar.projectKey=sonarDEVOPS -Dsonar.host.url=http://192.168.1.182:9000 -Dsonar.login=3b3f0f08cb863a3506325c71d50d09e8a4940116"
            }
        }
        stage('step 4 : Nexus') {
            steps {
                sh "mvn clean package -DskipTests deploy:deploy-file -DgroupId=tn.esprit -DartifactId=achat -Dversion=1.0 -DgeneratePom=true -Dpackaging=war -DrepositoryId=deploymentRepo -Durl=http://192.168.1.182:8081/repository/maven-releases/ -Dfile=target/achat-1.0.jar"
            }
        } 

     /*  stage('BUILD') { 
            steps { 
                script { 
                    timestamps {
                    dockerImage = docker.build medtouijer/devops
                    }
                }
            } 
        }
     */
         stage('PUSH DOCKERHUB') { 
            steps { 
                script {
                        timestamps {
						  docker.withRegistry ('', medtouijer/devops ) {
							  dockerImage.push()
                        }
                    } 
                }
            } 
            
        }


            }
        }

        
