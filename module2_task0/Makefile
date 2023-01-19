
build: ### build a exeutable file
		go build
clean: ### remuve the executable file
		-rm awesome-api
		-rm awesome-api.log
stop: ### stop the app in the server
		kill "$(shell pgrep awesome-api)"
test: ### unit test for the api
		-curl http://localhost:9999
		-curl http://localhost:9999/health
run: ### run the app in the local server
		./awesome-api >./awesome.log 2>&1 &