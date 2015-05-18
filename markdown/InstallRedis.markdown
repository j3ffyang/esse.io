## Pull Redis
	docker run --name=redis-gitlab -d -v=/pool/redis:/var/lib/redis sameersbn/redis:latest	


/pool is an extra mount from separated partition storage
