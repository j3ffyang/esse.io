## Install PostgreSQL

Reference > [https://registry.hub.docker.com/_/postgres/](https://registry.hub.docker.com/_/postgres/)

PostgreSQL is supposed to run a dedicated partition, which is mounted to operating system separatedly. In my case, the path mounted for PostgreSQL data

	/pool/postgresql 

The default path that contains database	

	/var/lib/postgresql/data 

## Pull and Configure PostgreSQL
	docker run --name='gitlab' -d --link=postgresql-gitlab:postgresql --link=redis-gitlab:redisio \
	--publish=10022:22 --publish=10080:80 --env='GITLAB_PORT=10080' --env='GITLAB_SSH_PORT=10022' \
	--volume=/pool/gitlab:/home/git/data sameersbn/gitlab:7.10.4
	
## Create a Database

	docker run --name=postgresql-gitlab -d --env='DB_NAME=gitlab' --env='DB_USER=gitlab' --env='DB_PASS=secret' \
	--volume=/pool/postgresql:/var/lib/postgresql sameersbn/postgresql:9.4		

From now on, you can access http://IP_ADDR:10080

## Data Store
Since GitLab data is stored at /home/git/data, which is mounted to /pool/gitlab, the path "/pool/gitlab" is the actual data source. You should backup this mount point to keep your repo data safe.
