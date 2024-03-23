.PHONY: buildup
buildup:
	docker compose -f docker-compose.yml up -d --build

.PHONY: down
down:
	docker compose -f docker-compose.yml down

.PHONY: build-image
build-image:
	docker build -t webserver .

.PHONY: shell
shell:
	docker compose -f docker-compose.yml exec -it nginx bash
