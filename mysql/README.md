# MySql

This is an exaple of a Dockerfile that use the software collection that exists in the catalog of OCP 3.11


```sh
# Creating a custom image for this
$ docker pull registry.access.redhat.com/rhscl/mysql-57-rhel7

# Running the container
$ docker run -d --name mysql_database -e MYSQL_USER=user -e MYSQL_PASSWORD=pass -e MYSQL_DATABASE=db -p 3306:3306 mysql-test

# Testing the image
$ docker exec -it mysql_database bash
bash-4.2$ MYSQL_PWD="$MYSQL_PASSWORD" mysql -h 127.0.0.1 -u $MYSQL_USER -D $MYSQL_DATABASE -e 'SELECT 1'
+---+
| 1 |
+---+
| 1 |
+---+
bash-4.2$
```
Now we can add it to openshift using the default values that exists in the *Dockerfile*

```sh
$ oc new-app --name mysql-database \
  --context-dir="mysql" \
  --strategy=docker \
  https://github.com/jorge-romero/databases-tests.git 
```


Or we can add the default values for user, password and database from a secret:

```sh
$ oc create secret generic mysql-database-secrets \
  --from-literal MYSQL_USER=usuario \
  --from-literal MYSQL_PASSWORD=password \
  --from-literal MYSQL_DATABASE=socksdb

secret/mysql-database-secrets created

$ oc set env dc/mysql-database \
  --from secret/mysql-database-secrets

deploymentconfig.apps.openshift.io/mydb updated
```

