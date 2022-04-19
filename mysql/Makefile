include .env
-include .env.local

APP_NAME=app

DOCKER_IMAGE=mysql
DOCKER_TAG=8.0

DOCKER_CONTAINER=${APP_NAME}-${DOCKER_IMAGE}-${DOCKER_TAG}
DOCKER_VOLUME=${DOCKER_CONTAINER}-data

pull:
	docker pull "${DOCKER_IMAGE}:${DOCKER_TAG}"

run:
	docker volume create "${DOCKER_VOLUME}"
	docker run --name "${DOCKER_CONTAINER}" \
		--detach \
		--env MYSQL_DATABASE="${DB_NAME}" \
		--env MYSQL_PASSWORD="${DB_PASS}" \
		--env MYSQL_ROOT_PASSWORD="${DB_PASS}" \
		--env MYSQL_USER="${DB_USER}" \
		--rm \
		--user `id -u`:`id -g` \
		--volume "${DOCKER_VOLUME}":/var/lib/mysql \
		"${DOCKER_IMAGE}:${DOCKER_TAG}" \
		--character-set-server=utf8mb4 \
		--collation-server=utf8mb4_unicode_ci \
	;

exec:
	docker exec -it "${DOCKER_CONTAINER}" mysql \
		--host="${DB_HOST}" \
		--password="${DB_PASS}" \
		--port="${DB_PORT}" \
		--user="${DB_USER}" \
		"${DB_NAME}" \
	;

stop:
	docker stop "${DOCKER_CONTAINER}"

rmi:
	docker rmi "${DOCKER_IMAGE}:${DOCKER_TAG}"

volume-rm:
	docker volume rm "${DOCKER_VOLUME}"
