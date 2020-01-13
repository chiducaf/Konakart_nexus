pipeline {
    agent any
    tools { 
        maven 'apache-maven-3.6.3' 
        jdk 'jdk1.8.0_192' 
    }
    stages {
        stage ('Initialize') {
            steps {
                
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            
            }
        }
        
       
       stage('Code Checkout') {
            steps { 
                
               git credentialsId: url: 'https://github.com/chiducaf/Action.git'
            }
        }
    
        

        stage ('Build') {
            steps {
                bat 'mvn -Dmaven.test.failure.ignore=true install' 
            }
			post {
                success {
                    junit 'target/surefire-reports/**/*.xml' 
                }
            }
            
        }
        
      //stage('SonarQube analysis') {
        //    steps {
          //      withSonarQubeEnv('sonar') {
                    // Optionally use a Maven environment you've configured already
                   
            //            bat 'mvn sonar:sonar'
              //      }
                //}
            //}
        stage ('Artifacts Upload to Archiva') {
            steps {
               // echo "Deploying"
              
               //bat 'echo %CD%'  
               
            //bat 'del D:\\apache-tomcat-7.0.92-windows-x64\\apache-tomcat-7.0.92\\webapps\\konakart.war'
			//bat 'del D:\\apache-tomcat-7.0.92-windows-x64\\apache-tomcat-7.0.92\\webapps\\konakart'
		   // sleep 20
		   bat 'mvn deploy'
            }
        }
	    
	   
        stage ('Deploy To Server') {
            steps {
                echo "Deploying"
              
             bat 'del D:\\apache-tomcat-7.0.92-windows-x64\\apache-tomcat-9.2.27\\webapps\\konakart.war'
             sleep 20
             bat '''cd target
            copy konakart.war D:\\apache-tomcat-7.0.92-windows-x64\\apache-tomcat-9.2.27\\webapps
            '''
            sleep 20
            }
        }
		
		stage ('Functional test') {
            steps {
                echo "Test Started"
              
               //bat 'echo %CD%'  
               
             bat '''d:
             
            cd D:\\EKART\\
            Run.bat
            
            '''
           
            }
        }
        
}
    }

