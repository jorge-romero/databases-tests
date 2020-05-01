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



