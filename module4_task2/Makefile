.PHONY: build
clean: ##Cleanup the content of the directory dist/
	@-make stop
	@-rm -rf awesome-api awesome.log coverage* go* ./dist

build: ## build everything
	@make go-build
	@make hugo-build

go-build: ## build go
	@sudo docker run --rm --volume=$(shell pwd):/app --workdir=/app awesome:build go mod init github.com/Ragnar9902/awesome-api
	@sudo docker run --rm --volume=$(shell pwd):/app --workdir=/app awesome:build go get github.com/gorilla/mux
	@sudo docker run --rm --volume=$(shell pwd):/app --workdir=/app awesome:build go build

hugo-build:  ##build hugo 
	@sudo docker run --rm --volume=$(shell pwd):/app --workdir=/app awesome:build hugo

post: ##Create a new blog post whose filename and title come from the environment variables POST_TITLE and POST_NAME.
	@sudo docker run --rm --volume=$(shell pwd):/app --workdir=/app awesome:build hugo new posts/${POST_NAME}.md
	@sudo docker run --rm --volume=$(shell pwd):/app --workdir=/app awesome:build sed -i "s/title: .*/title: ${POST_TITLE}/" ./content/posts/${POST_NAME}.md
help: ##shows commands usage information
	@fgrep -h "##" $(MAKEFILE_LIST) | fgrep -v fgrep | sed -e 's/\\$$//' | sed -e 's/##//'

check: ## test the app
	@sudo docker run --rm --volume=$(shell pwd):/app --workdir=/app awesome:build markdownlint ./content/posts/*.md
	@sudo docker run --rm --volume=$(shell pwd):/app --workdir=/app awesome:build markdown-link-check ./content/posts/*.md
package: build  ## Generates a zip archive and a docker image to deployment
	docker build -t awesome:${IMAGE_TAG} .
	docker save -o awesome_image.tar awesome:${IMAGE_TAG}
	zip awesome-website.zip awesome-api dist/ awesome_image.tar
validate: ## W3C validator
	-make build
	-git clone https://github.com/holbertonschool/W3C-Validator.git
	-./W3C-Validator/w3c_validator.py ./dist/index.html
	-rm -rf ./W3C-Validator

test: ## Tests the application
	@-make build
	@make unit-tests
	@make integration-tests

lint: ## make lint on the files
	-make build-docker
	sudo docker run --rm --volume=$(shell pwd):/app --workdir=/app awesome:build markdownlint README.md DEPLOY.md
	sudo docker run --rm --volume=$(shell pwd):/app --workdir=/app awesome:build hadolint --ignore DL4001 build/Dockerfile
unit-tests: ## make unit tests on the files
	@sudo docker run --rm --volume=$(shell pwd):/app --workdir=/app awesome:build go test -v -short -coverprofile=coverage-units.out

integration-tests: ## make unit tests on the files
	@sudo docker run --rm --volume=$(shell pwd):/app --workdir=/app awesome:build go test -v -coverprofile=coverage-integrations.out

run: ## Runs the application in background
	@./awesome-api >./awesome.log 2>&1 &
build-docker:	## Builds a Docker image from Dockerfile on build directory
	@sudo docker build -t awesome:build ./build

stop: ## Stops the application
	@kill $(shell pgrep awesome-api) 2>&1 &
docker-tests:	## Test the generated docker image using container-structure-test and cst.yml config file
	-make build-docker
	container-structure-test test --image awesome:build --config build/cst.yml