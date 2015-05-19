## Create SSL

### Create the server private key

	openssl genrsa -out gitlab.key 2048	

### Create the certificate signing request (CSR)

	openssl req -new -key gitlab.key -out gitlab.csr

### Sign the certificate using the private key and CSR

	openssl x509 -req -days 365 -in gitlab.csr -signkey gitlab.key -out gitlab.crt	

### Generate Stronger DHE Parameters.
To strength the server security, we need to generate stronger DHE parameters.

	openssl dhparam -out dhparam.pem 2048	

## Installation of the SSL Certificates

	mkdir -p /pool//gitlab/certs
	cp gitlab.key /pool/gitlab/certs/
	cp gitlab.crt /pool/gitlab/certs/
	cp dhparam.pem /pool/gitlab/certs/
	chmod 400 /pool/gitlab/certs/gitlab.key	

## Apply the Change

	docker ps	
	docker rm gitlab

	docker run --name='gitlab' -d --link=postgresql-gitlab:postgresql --link=redis-gitlab:redisio \
		--publish=10022:22 --publish=10080:80 --env='GITLAB_PORT=10080' --env='GITLAB_SSH_PORT=10022' \
		--env='GITLAB_HTTPS=true' --env='SSL_SELF_SIGNED=true' --volume=/pool/gitlab:/home/git/data \
		sameersbn/gitlab:7.10.4


## Enable HSTS to Force All Traffic to Go through HTTPS

	--env='GITLAB_HTTPS_HSTS_MAXAGE=2592000'

	docker run --name='gitlab' -d --link=postgresql-gitlab:postgresql --link=redis-gitlab:redisio \
		--publish=10022:22 --publish=10443:443 --env='GITLAB_PORT=443' --env='GITLAB_SSH_PORT=10022' \
		--env='GITLAB_HTTPS=true' --env='SSL_SELF_SIGNED=true' --env='GITLAB_HTTPS_HSTS_MAXAGE=2592000' \
		--volume=/pool/gitlab:/home/git/data sameersbn/gitlab:7.10.4 
