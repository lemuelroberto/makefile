include .env
-include .env.local

MYSQL_IMAGE=mysql
MYSQL_VERSION=8.0
DOCKER_PREFIX=app
DOCKER_NAME="${DOCKER_PREFIX}-mysql"
DOCKER_VOLUME="${DOCKER_PREFIX}-mysql-data"

mysql-pull:
	docker pull "${MYSQL_IMAGE}":"${MYSQL_VERSION}"

mysql-run:
	docker volume create "${DOCKER_VOLUME}"
	docker run --name "${DOCKER_NAME}" \
		--detach \
		--env MYSQL_DATABASE="${DB_NAME}" \
		--env MYSQL_PASSWORD="${DB_PASS}" \
		--env MYSQL_ROOT_PASSWORD="${DB_PASS}" \
		--env MYSQL_USER="${DB_USER}" \
		--rm \
		--user `id -u`:`id -g` \
		--volume "${DOCKER_VOLUME}":/var/lib/mysql \
		"${MYSQL_IMAGE}":"${MYSQL_VERSION}" \
		--character-set-server=utf8mb4 \
		--collation-server=utf8mb4_unicode_ci \
	;

mysql-exec:
	docker exec -it "${DOCKER_NAME}" mysql \
		--host="${DB_HOST}" \
		--password="${DB_PASS}" \
		--port="${DB_PORT}" \
		--user="${DB_USER}" \
		"${DB_NAME}" \
	;

mysql-stop:
	docker stop "${DOCKER_NAME}"

mysql-rmi:
	docker rmi "${MYSQL_IMAGE}":"${MYSQL_VERSION}"

mysql-volume-rm:
	docker volume rm "${DOCKER_VOLUME}"
