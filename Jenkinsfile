pipeline    /* installation on master and deployment on slave */
{
     agent{
	        label{
				label "built-in"
			}
		}
		
		stages {
			stage("installation"){
					steps{
						sh "sudo su -"
						sh "yum install git -y"
						sh "yum install java-1.8.0-openjdk-devel.x86_64 -y"
						sh "yum install maven -y"
						sh "yum install docker -y"
						sh "service docker start"
					}
			}
			stage("tomcat-installation"){
							steps{
								sh "cd /mnt/server"
								sh "wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.72/bin/apache-tomcat-9.0.72.zip"
								sh "unzip apache-tomcat-9.0.71.zip"
								sh "rm -rf apache-tomcat-9.0.71.zip"
								sh "cd apache-tomcat-9.0.71/webapps"
								sh "wget https://get.jenkins.io/war-stable/2.346.3/jenkins.war"
								sh "cd /mnt/server/apache-tomcat-9.0.71/bin"
								sh "chmod 777 *"
								sh "./startup.sh"
							}
			}
			stage("clone&packaging"){
						steps{
						    dir("/mnt/game"){
									sh "git clone https://github.com/Shantanumajan6/game-of-life.git"
									sh "chmod -R 777 /mnt/game"
									}
							dir("/mnt/game/game-of-life/"){
									sh "mvn clean install"
									}

							}
						}
			stage("Deployment"){
						steps{
							sh "cp -r /mnt/game/game-of-life/gameoflife-web/target/gameoflife.war /mnt/server/apache-tomcat-9.0.71/webapps"
						}
					}
				}
}		
