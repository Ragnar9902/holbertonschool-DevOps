clean: ## Cleanup the content of the directory dist/
		@rm -rf dist
build: ## Generate the website from the markdown and configuration files in the directory dist/
		@make check 
		@hugo
post: ## Create a new blog post whose filename and title come from the environment variables POST_TITLE and POST_NAME.
		@hugo new posts/${POST_NAME}.md
		@sed -i "s/title: .*/title: ${POST_TITLE}/" ./content/posts/${POST_NAME}.md
check: ## test the app
		@markdownlint ./content/posts/*.md
		@markdown-link-check ./content/posts/*.md
validate: ## W3C validator
		@make build
		@./w3c_validator.py ./dist/index.html || true
help: ##shows commands usage information
		@fgrep -h "##" $(MAKEFILE_LIST) | fgrep -v fgrep | sed -e 's/\\$$//' | sed -e 's/##//'