## Install GitLab

## Pull GitLab
	docker pull sameersbn/gitlab:7.10.4	

## Start GitLab
After Postgre and Redis have been configured properly

	docker run --name='gitlab' -d --link=postgresql-gitlab:postgresql --link=redis-gitlab:redisio \
	--publish=10022:22 --publish=10080:80 --env='GITLAB_PORT=80' --env='GITLAB_SSH_PORT=10022' \
	--env='SSL_SELF_SIGNED=true' --volume=/pool/gitlab:/home/git/data sameersbn/gitlab:7.10.4

