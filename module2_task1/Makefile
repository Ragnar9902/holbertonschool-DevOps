build: ## build a exeutable file
	@go build
clean: ## remuve the executable file
	@make stop
	@rm awesome-api 2>&1 &
	@rm awesome-api.log 2>&1 &
stop: ## stop the app in the server
	@kill "$(shell pgrep awesome-api)" 2>&1 &
test: ## unit test for the api
	@curl http://localhost:9999
	@curl http://localhost:9999/health
run: ## run the app in the local server
	@./awesome-api >./awesome.log 2>&1 &
lint: ## make lint on the files
	@sudo docker run --rm --volume=$(shell pwd):/app --workdir=/app awesome:build golangci-lint run
help: ## Show this help.
	@fgrep -h "##" $(MAKEFILE_LIST) | fgrep -v fgrep | sed -e 's/\\$$//' | sed -e 's/##//'
build-docker:	## Builds a Docker image from Dockerfile on build directory
	@sudo docker build -t awesome:build .