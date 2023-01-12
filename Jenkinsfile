pipeline {
    agent any
    stages {
        stage('step 1 : Clone code from Git') {
            steps {
                echo "GitHub clone step"
                git branch: "aymen",
                url: "https://github.com/aymenESP/achatDEVOPS.git"
            }
        }
        stage('step 2 : Compile & test Maven') {
            steps {
                sh 'mvn clean compile -DskipTests'
                sh 'mvn test'
            }
        }
        stage('step 3 : Run SonarQube') {
            steps {
                sh   "mvn sonar:sonar -Dsonar.projectKey=devopsproject -Dsonar.host.url=http://192.168.184.130:9000 -Dsonar.login=661442f6ec8861168f9cd6c321aa6c2812f20489"
            }

          
        }
        stage('step 4 : Deploy to Nexus') {
            steps {
                sh "mvn clean package -DskipTests deploy:deploy-file -DgroupId=tn.esprit -DartifactId=achat -Dversion=1.0 -DgeneratePom=true -Dpackaging=war -DrepositoryId=deploymentRepo -Durl=http://192.168.184.130:8081/repository/maven-releases/ -Dfile=target/achat-1.0.jar"
            }
        }
}
}
