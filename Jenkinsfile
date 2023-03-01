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
						sh "sudo yum install git -y"
						sh "sudo yum install maven -y"
						sh "sudo yum install docker -y"
						sh "service docker start"
					}
			}
			stage("clone&packaging"){
						steps{
					   		sh "rm -rf /mnt/game"
							sh "cd /mnt/"
							sh "git clone https://github.com/Shantanumajan6/game-of-life.git"
							sh "chmod -R 777 /mnt/game"

							}
						}
			stage("Deployment"){
						steps{
							sh "cp -r /mnt/game/game-of-life/gameoflife-web/target/gameoflife.war /mnt/server/apache-tomcat-9.0.71/webapps"
						}
					}
				}
}		
