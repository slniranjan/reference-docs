CONNECT TO MYSQL DATABASE FROM COMMAND LINE
```
mysql -h 172.17.0.2 -u USERNAME -p
```
When using dBeaver MySQL 8+ connection
```
Add two properties: "useSSL" and "allowPublicKeyRetrieval"
Set their values to  "false" and "true"
