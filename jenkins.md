sudo /etc/init.d/jenkins start

nohup /home/sonarqube/sonarqube-9.4.0.54424/bin/linux-x86-64/sonar.sh start > /home/sonarqube/sonarqube-9.4.0.54424/logs/sonar.out 2>&1 &

screen -S sonarqube

./sonar.sh console

jenkins uname admin pwd admin
