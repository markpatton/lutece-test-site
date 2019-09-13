
# Install dependencies

Need mysql and tomcat

On Fedora linux
```
dnf install community-mysql-server.x86_64 tomcat tomcat-native
service mysqld start
service tomcat start
```

# Create database

```
CREATE USER 'lutece'@'localhost' IDENTIFIED BY 'lutece';
create database lutece;
GRANT ALL PRIVILEGES ON lutece.* TO 'lutece'@'localhost';
```

# Init db in  /webapps/lutece/WEB-INF/sql

```
cat create_db_lutece_core.sql init_db_lutece_core.sql | mysql -u lutece -p lutece
cat $(find plugins -name 'create_*.sql') | mysql -u lutece -p lutece
cat $(find plugins -name 'init_*.sql') | mysql -u lutece -p lutece
```

# Package up app and deploy

```
mvn clean lutece:site-assembly

```

Unnpack war to /webapps/lutece in tomcat.

# Set db user and pass in webapp

Edit  /webapps/lutece/WEB-INF/conf/db.properties

# Login to site

User: admin
Password: adminadmin

http://localhost:8080/example/jsp/admin/AdminLogin.jsp