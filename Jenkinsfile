pipeline    /* installation on master and deployment on slave */
{
     agent{
	        label{
				label "built-in"
				customWorkspace "/mnt/game"
			}
		}
		
		stages{
			stage("installation"){
					steps{
						sh "sudo su -"
						sh "sudo yum install git -y"
						sh "sudo yum install maven -y"
						sh "sudo yum install docker -y"
						sh "service docker start"
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
