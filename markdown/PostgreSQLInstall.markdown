## Install PostgreSQL

Reference > [https://registry.hub.docker.com/_/postgres/](https://registry.hub.docker.com/_/postgres/)

PostgreSQL is supposed to run a dedicated partition, which is mounted to operating system separatedly. In my case, the path mounted for PostgreSQL data

	/pool/postgresql 

The default path that contains database	

	/var/lib/postgresql/data 

## Launch PostgreSQL

	docker run --name=postgresql-gitlab -d --env='DB_NAME=gitlab' --env='DB_USER=gitlab' --env='DB_PASS=mysecret' \
		--volume=/data/postgresql:/var/lib/postgresql sameersbn/postgresql:9.4

## Data Store
Since GitLab data is stored at /home/git/data, which is mounted to /pool/gitlab, the path "/pool/gitlab" is the actual data source. You should backup this mount point to keep your repo data safe.

## Create Database in External PostgreSQL

	su - postgres
	psql

	postgres=# create database gitlabhq_production;             
	CREATE DATABASE
	gitlab=# \l
	                                  List of databases
	        Name         |  Owner   | Encoding | Collate | Ctype |   Access privileges   
	---------------------+----------+----------+---------+-------+-----------------------
	 gitlab              | postgres | UTF8     | C       | C     | =Tc/postgres         +
	                     |          |          |         |       | postgres=CTc/postgres+
	                     |          |          |         |       | gitlab=CTc/postgres
	 gitlabhq_production | gitlab   | UTF8     | C       | C     | 
	 postgres            | postgres | UTF8     | C       | C     | 
	 template0           | postgres | UTF8     | C       | C     | =c/postgres          +
	                     |          |          |         |       | postgres=CTc/postgres
	 template1           | postgres | UTF8     | C       | C     | =c/postgres          +
	                     |          |          |         |       | postgres=CTc/postgres
	(5 rows)
	
	postgres=# grant all privileges on database gitlabhq_production to gitlab;
	
