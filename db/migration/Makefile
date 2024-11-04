export $(shell sed 's/=.*//' .env)
postgres:
	docker run --name ${CONTAINER_NAME} -p 5432:5432 -e POSTGRES_USER=${POSTGRES_USER} -e POSTGRES_PASSWORD=4{POSTGRES_PASSWORD} -d postgres:12-alpine

createdb:
	docker exec -it ${CONTAINER_NAME} createdb --username=${POSTGRES_USER} --owner=${POSTGRES_USER} ${DATABASE_NAME}

dropdb:
	docker exec -it ${CONTAINER_NAME} dropdb ${DATABASE_NAME}

migrateup:
	migrate -path db/migration -database "postgresql://${POSTGRES_USER}:${POSTGRES_PASSWORD}@localhost:5432/${DATABASE_NAME}?sslmode=disable" -verbose up

migratedown:
	migrate -path db/migration -database "postgresql://${POSTGRES_USER}:${POSTGRES_PASSWORD}@localhost:5432/${DATABASE_NAME}?sslmode=disable" -verbose down

.PHONY: createdb dropdb migrateup migratedown postgres