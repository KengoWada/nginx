.PHONY: buildup
buildup:
	docker compose -f docker-compose.yml up -d --build

.PHONY: build
build:
	docker compose -f docker-compose.yml build

.PHONY: up
up:
	docker compose -f docker-compose.yml up

.PHONY: down
down:
	docker compose -f docker-compose.yml down

.PHONY: build-image
build-image:
	docker build -t webserver .

.PHONY: shell
shell:
	docker compose -f docker-compose.yml exec -it nginx bash
