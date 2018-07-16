ENV = docker-compose run --rm app

.PHONY: run setup test build

setup: qlfile
	$(ENV) qlot install
	$(ENV) qlot bundle

test: setup t/%.lisp src/%.lisp
	$(ENV) qlot exec ros -l "/app/bundle-libs/bundle.lisp" -S . -Q -e '(ql:quickload :<% @var name %>-test)' -q

build: Dockerfile docker-compose.yml
	docker-compose build

run:
	docker-compose up
