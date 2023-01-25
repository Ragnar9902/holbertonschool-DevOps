clean: ##Cleanup the content of the directory dist/
	@-make stop
	@-rm -rf awesome-api awesome.log coverage* go* ./dist

build: ## build everything
	-make go-build
	@make hugo-build

go-build: ## build go
	@go mod init github.com/paosua86/awesome-api
	@go get github.com/gorilla/mux
	@go build

hugo-build:  ##build hugo 
	@hugo

post: ##Create a new blog post whose filename and title come from the environment variables POST_TITLE and POST_NAME.
	@hugo new posts/${POST_NAME}.md
	@sed -i "s/title: .*/title: ${POST_TITLE}/" ./content/posts/${POST_NAME}.md
help: ##shows commands usage information
	@fgrep -h "##" $(MAKEFILE_LIST) | fgrep -v fgrep | sed -e 's/\\$$//' | sed -e 's/##//'

check: ## test the app
	@markdownlint ./content/posts/*.md
	@markdown-link-check ./content/posts/*.md
validate: ## W3C validator
	@make build
	@./w3c_validator.py ./dist/index.html || true

test: ## Tests the application
	@-make build
	@make unit-tests
	@make integration-tests

lint: ## make lint on the files
	@golangci-lint run

unit-tests: ## make unit tests on the files
	sudo docker run --rm --volume=$(shell pwd):/app --workdir=/app golang:1.15.8-buster go test -v -short -coverprofile=coverage-units.out

integration-tests: ## make unit tests on the files
	sudo docker run --rm --volume=$(shell pwd):/app --workdir=/app golang:1.15.8-buster go test -v -coverprofile=coverage-integrations.out


run: ## Runs the application in background
	@./awesome-api >./awesome.log 2>&1 &

stop: ## Stops the application
	@kill $(shell pgrep awesome-api) 2>&1 &