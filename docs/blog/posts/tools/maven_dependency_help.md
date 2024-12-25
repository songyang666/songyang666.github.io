---
date:
  created: 2024-12-24
categories:
  - Maven
readtime: 1
authors:
  - charlie
---
# 利用mvn dependency 命令查询依赖
```bash
# mvn dependency:tree -Dincludes=groupId:artifactId
# mvn dependency:tree -Dincludes=ch.qos.logback -o
# mvn dependency:tree -Dincludes=org.springframework:spring-core
 mvn -o dependency:tree -Dincludes=commons-logging 
```
