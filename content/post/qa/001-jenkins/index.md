---
categories: []
tags: ["QA","Jenkins","GITLAB"]
description: ""
menu: 
    main:
        parent: "QA testing"
date: "2017-11-20T23:27:56+03:00"
title: "Работа с Jenkins"
---

**Jenkins** - инструмент автоматизации. Бесплатен. 
Groovy  в качестве встроенного языка сценариев.
Большое число plugin. Большое сообщество.
Расширяем, но требует Java VM для работы.
<!--more-->

#### Show version
```$ java -jar /var/cache/jenkins/war/WEB-INF/jenkins-cli.jar -s http://localhost:8080/ version```


#### Upgrade
> 
```$ wget http://updates.jenkins-ci.org/download/war/2.26/jenkins.war```
```# ls -al /usr/share/jenkins/jenkins.war ```
-rw-r--r-- 1 root root 63350272 Jan 19  2016 /usr/share/jenkins/jenkins.war
```# cp  /usr/share/jenkins/jenkins.war /usr/share/jenkins/jenkins.war.previous.version```
```# cp  ./jenkins.war /usr/share/jenkins/jenkins.war```


#### Restart
```# java -jar /var/cache/jenkins/war/WEB-INF/jenkins-cli.jar -s http://localhost:8080/ restart```

после включение Config Global Sequrity - Enable - Anyone 
можно ходить с локальной машины на удаленный дженкинс
```# java -jar jenkins-cli.jar -s http://10.0.2.175:8080/ version ```


#### Groovy pipeline
> node {
    stage 'Does sshpass work?'
    sh 'sshpass -p \'password\' ssh user@host "ls; hostname; whois google.com;"'
}
