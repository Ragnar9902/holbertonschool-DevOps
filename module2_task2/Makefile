
build: ## build a exeutable file
	@sudo docker run --rm --volume=$(shell pwd):/app --workdir=/app awesome:build go build
clean: ## remuve the executable file
	@make stop
	@rm awesome-api 2>&1 &
	@rm awesome-api.log 2>&1 &
lint: ## test the app
	@sudo docker run --rm --volume=$(shell pwd):/app --workdir=/app awesome:build golangci-lint run
build-docker:	## Builds a Docker image from Dockerfile on build directory
	@sudo docker build -t awesome:build ../
unit-tests: ## make unit tests on the files
	@go test -v -short -coverprofile=coverage-units.out || echo $1
stop: ## stop the app in the server
	@kill "$(shell pgrep awesome-api)" 2>&1 &
test: ## custom test for the api
	@curl http://localhost:9999
	@curl http://localhost:9999/health
	@curl http://localhost:9999/hello
run: ## run the app in the local server
		@./awesome-api >./awesome.log 2>&1 &
help: ## Show this help.
	@fgrep -h "##" $(MAKEFILE_LIST) | fgrep -v fgrep | sed -e 's/\\$$//' | sed -e 's/##//'