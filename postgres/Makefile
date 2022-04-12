include .env
-include .env.local

APP_NAME=app
DOCKER_IMAGE=postgres
DOCKER_TAG=14.2

DOCKER_CONTAINER=${APP_NAME}-${DOCKER_IMAGE}-${DOCKER_TAG}
DOCKER_VOLUME=${DOCKER_CONTAINER}-data

pull:
	docker pull ${DOCKER_IMAGE}:${DOCKER_TAG}

run:
	docker run --name ${DOCKER_CONTAINER} \
		--detach \
		--env POSTGRES_DB=${DB_NAME} \
		--env POSTGRES_PASSWORD=${DB_PASS} \
		--env POSTGRES_USER=${DB_USER} \
		--rm \
		--volume ${DOCKER_VOLUME}:/var/lib/postgresql/data \
		${DOCKER_IMAGE}:${DOCKER_TAG} \
	;

exec:
	docker exec -it ${DOCKER_CONTAINER} psql \
		postgresql://${DB_USER}:${DB_PASS}@${DB_HOST}:${DB_PORT}/${DB_NAME} \
	;

stop:
	docker stop ${DOCKER_CONTAINER}

rmi:
	docker rmi ${DOCKER_IMAGE}:${DOCKER_TAG}

volume-rm:
	docker volume rm ${DOCKER_VOLUME}
