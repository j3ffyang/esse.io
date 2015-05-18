## Install PostgreSQL

Reference > [https://registry.hub.docker.com/_/postgres/](https://registry.hub.docker.com/_/postgres/)

PostgreSQL is supposed to run a dedicated partition, which is mounted to operating system separatedly. In my case, /pool/postgresql is created and mounted for PostgreSQL data

/var/lib/postgresql/data is default path that contains database

## Pull PostgreSQL
	docker run --name='gitlab' -d --link=postgresql-gitlab:postgresql --link=redis-gitlab:redisio \
	--publish=10022:22 --publish=10080:80 --env='GITLAB_PORT=10080' --env='GITLAB_SSH_PORT=10022' \
	--volume=/pool/gitlab:/home/git/data sameersbn/gitlab:7.10.4
	

