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
# mvn dependeny:tree -Dincludes=groupId:artifactId:version
 mvn -o dependency:tree -Dincludes=commons-logging 
```
