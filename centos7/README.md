MariaDB Dockerfile
==================

[![N|Solid](http://sgs.shrigowri.com/wp-content/uploads/2017/05/cropped-orange2-2-1-1-32x32.png)Shri Gowri Solutions LLP](http://shrigowri.com)

Based on CentOS7 original mariadb Dockerfile...

This repo contains a recipe for making Docker container for mariadb on CentOS7.

Setup
-----

Check your Docker version

    # docker version

Perform the build

    # docker build --rm --tag <tagname>/mariadb55 .

Check the image out.

    # docker images

Launching MariaDB
-----------------

### Quick start (not recommended for production use): ###

    # docker run --name=mariadb -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=<password> <tagname>/mariadb

### Recommended start ###

To use a separate data volume for /var/lib/mysql (recommended, to allow image update without
losing database contents):

Create a data volume container: (it doesn't matter what image you use
here, we'll never run this container again; it's just here to
reference the data volume)

    # docker run --name=mariadb-data -v /var/lib/mysql <tagname>/mariadb55 true

And now create the daemonized mariadb container:

    # docker run --name=mariadb -d -p 3306:3306 --volumes-from=mariadb-data -e MYSQL_ROOT_PASSWORD=<password> <tagname>/mariadb55

You could also create an additional database by passing MYSQL_DATABASE and/or create an additional user passing MYSQL_USER to the container.
You can specify database character set and/or collation by specifying MYSQL_CHARSET and/or MYSQL_COLLATION!

Using your MariaDB container
----------------------------

know the ip address of the container

docker inspect <containerid> | grep -i ipaddr

Connecting to mariadb:

    # mysql -h 172.17.0.2 -uroot -p<password>

Create a sample Database:	

	\> CREATE SCHEMA sampleDb
Create a sample table:

    \> CREATE TABLE sampleDb.test (name VARCHAR(10), owner VARCHAR(10),
        -> species VARCHAR(10), birth DATE, death DATE);
License
----

MIT