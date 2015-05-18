## Change GitLab Mail Default Passwd

	docker run --name=gitlab -d \
	--env='SMTP_USER=USER@gmail.com' --env='SMTP_PASS=PASSWORD' \ 
	--volume=/srv/docker/gitlab/gitlab:/home/git/data \ sameersbn/gitlab:7.10.4	


