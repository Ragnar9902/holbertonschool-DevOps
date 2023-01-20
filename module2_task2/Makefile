
build: ## build a exeutable file
		go build
clean: ## remuve the executable file
		make stop
		-rm awesome-api
		-rm awesome-api.log
lint: ## test the app
unit-test: ## unit test
		go test -v -short -coverprofile=coverage-units.out
stop: ## stop the app in the server
		kill "$(shell pgrep awesome-api)"
test: ## custom test for the api
		curl http://localhost:9999
		curl http://localhost:9999/health
		curl http://localhost:9999/hello
run: ## run the app in the local server
		./awesome-api >./awesome.log 2>&1 &
help: ## Show this help.
	@fgrep -h "##" $(MAKEFILE_LIST) | fgrep -v fgrep | sed -e 's/\\$$//' | sed -e 's/##//'