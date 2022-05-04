pipeline {
    agent any
    parameters{
        booleanParam description: 'Do you want Jenkins to deploy war on TomCat after building?', name: 'Deploy'
        string defaultValue: 'CourseProject23', description: 'The exact value of "Context path" to deploy', name: 'Name',trim: true
    }
    stages {
        stage('Info') {
            steps {
                    echo "Java version:"
                    sh   "java --version"
                    }
                }
        stage('Preparing') {
            steps {
               echo "Preparing for building:"
               git changelog: false, poll: false, url: 'https://github.com/Yamali23/CourseProject23'
               sh   "mvn clean"
               echo "Preparing completed"
            }
        }
        
        stage('Building') {
            steps {
               echo "Building project:"
               sh   "mvn package"
               echo "Build success"
            }
        }    
        stage('Deploying') {
            steps {
               script{
               if ("${params.Deploy}"=="true"){
                    echo "Deploying on TomCat:"
                    deploy adapters: [tomcat9(credentialsId: 'd7a6a324-46af-43da-a015-5fc459e50179', path: '', url: 'http://xn--e1afhkfagivn.xn--p1ai:8081/')],contextPath: "${params.Name}", war: '**/WindowsCalculator.war'
                    echo "Deployed successfully" 
                    }
                }  
                
            }
        }
    }
}
