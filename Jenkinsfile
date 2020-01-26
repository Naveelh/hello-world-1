pipeline { 

    agent any 

        stages { 

           stage('SCM Checkout') { 

               steps { 

                   git url:'https://github.com/Naveelh/hello-world-1.git' 

                       } 

                               } 

           stage('Build') { 

               steps { 

                        sh" /opt/maven/apache-maven-3.6.2/bin/mvn clean package -Dmaven.test.skip=true" 

                            } 

                    } 

           stage('Build Analysis') { 

               steps { 

                   withSonarQubeEnv('sonarqube-scanner')   

                          { 

                        sh "/opt/maven/apache-maven-3.6.2/bin/mvn clean verify sonar:sonar -Dmaven.test.skip=true" 

                             } 

                    } 

                } 

          /* stage("Quality Gate") { 

               steps { 

                  timeout(time: 50, unit: 'MINUTES') { 

                     waitForQualityGate abortPipeline: true 

                       } 

                  } 

              } */ 

           stage('Deploy') { 

               steps { 

                   sh" /opt/maven/apache-maven-3.6.2/bin/mvn clean deploy -Dmaven.test.skip=true" 

                             } 

                    } 

           stage('Release') { 

               steps { 

                   sh"export JENKINS_NODE_COOKIE=dontKillMe; nohup java -jar $WORKSPACE/target/*.jar &" 

                           } 

                    } 

                } 

            } 
