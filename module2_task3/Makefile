
build: ## build a exeutable file
		go build
clean: ## remuve the executable file
		@make stop
		@rm awesome-api 2>&1 &
		@rm awesome-api.log 2>&1 &
		@rm -r coverage-integrations.out 2>&1 &
		@rm -r coverage-units.out 2>&1 &
lint: ## test the app
unit-tests: ## unit test
		go test -v -short -coverprofile=coverage-units.out || echo $1
integration-tests: ## make integration tests 
		go test -v -short -coverprofile=coverage-integrations.out || echo $1
stop: ## stop the app in the server
		@kill "$(shell pgrep awesome-api)" 2>&1 &
test: ## custom test for the api
		curl http://localhost:9999
		curl http://localhost:9999/health
		curl http://localhost:9999/hello
run: ## run the app in the local server
		./awesome-api >./awesome.log 2>&1 &
help: ## Show this help.
	@fgrep -h "##" $(MAKEFILE_LIST) | fgrep -v fgrep | sed -e 's/\\$$//' | sed -e 's/##//'