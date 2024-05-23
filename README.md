# hive3 install on kubernetes

## 1. helm install
```bash
helm upgrade --install hive3 ./hive3-helm --namespace hive3 --set hive3.image.tag=3.1.0
```

## 2. check
```bash
kubectl get pods -n hive3
```

## 3. connect
```bash
kubectl exec -it hive3-hive-metastore-0 -n hive3 -- /bin/bash
```
## 4. create database
```bash
beeline -u jdbc:hive2://localhost:10000 -n hive -p hive
```
```sql
CREATE DATABASE IF NOT EXISTS test;
```

## 5. create table
```sql
CREATE TABLE IF NOT EXISTS test.test_table (id INT, name STRING);
```

## 6. insert data
```sql
INSERT INTO test.test_table VALUES (1, 'test');
```

## 7. select data
```sql
SELECT * FROM test.test_table;
```

## 8. uninstall
```bash
helm uninstall hive3 -n hive3
```