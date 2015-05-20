## Install GitLab

## Pull GitLab
	docker pull sameersbn/gitlab:7.10.4	

## Start GitLab
After Postgre and Redis have been configured properly

	docker run --name='gitlab' -d --link=postgresql-gitlab:postgresql --link=redis-gitlab:redisio \
		--publish=10022:22 --publish=10080:80 --env='GITLAB_PORT=80' --env='GITLAB_SSH_PORT=10022' \
		--env='SSL_SELF_SIGNED=true' --volume=/pool/gitlab:/home/git/data sameersbn/gitlab:7.10.4

## Start GitLab with OpenLDAP and SSL
Reference > https://github.com/sameersbn/docker-gitlab

	docker run --name='gitlab' -d --link=postgresql-gitlab:postgresql --link=redis-gitlab:redisio \
		--publish=10022:22 --publish=10443:443 --env='GITLAB_PORT=443' --env='GITLAB_SSH_PORT=10022' \
		--env='GITLAB_HTTPS=true' --env='SSL_SELF_SIGNED=true' --env='GITLAB_HTTPS_HSTS_MAXAGE=2592000' \
		--env='LDAP_ENABLED=yes' --env='LDAP_HOST=192.168.102.2' --env='LDAP_METHOD=ssl' \
		--env='LDAP_PASS=mysecret' --env='LDAP_ACTIVE_DIRECTORY=false' \
		--volume=/pool/gitlab:/home/git/data sameersbn/gitlab:7.10.4
