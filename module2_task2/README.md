build:  build a exeutable file
clean:  remuve the executable file
stop:  stop the app in the server
test:  unit test for the api
run:  run the app in the local server
lint: test the app
unit-test:  unit test
help:  Show this help.

# Prerequisites:

The following elements are required In addition to the previous module (“Module 1: Introduction to DevOps: Automate Everything to Focus on What Really Matters”) prerequisites.
Concepts

You should have a basic knowledge on the following concepts:

    What a compiled language is (C/C#/Golang/Rust/etc.)
        Generation process from source to executable binary
        Basic types: string, integer, boolean, maps, arrays
        Basic algorithmic: loops, conditional, functions

    Installing command line tools with NPM (in addition to package managers)

    Understand the basics of the HTTP protocol (client/server, verbs, headers)

Tooling

This project needs the following tools / services:

    Same tools as previous module
    Golang in v1.15.*
    NPM v7+ with NodeJS v14.* (stable)
    Python 3 with pip module
# Lifecycle:
The life-cycle of this project is the following:

    “Build”: compile the source code of the application to a binary named awesome-api (the name awesome-api comes from the command go mod init github.com/<your github handle>/awesome-api) with the command go build.

    “Run”: Run the application in background by executing the binary awesome-api, and write logs into a file named awesome.log with the command ./awesome-api >./awesome.log 2>&1 &.

    “Stop”: Stop the application with the command kill XXXXX where XXXXX is the Process ID of the application. For instance: kill "$(pgrep awesome-api)".

    “Clean”: Delete the binary awesome-api and the log file awesome-api.log

    “Test”: You want to test it to ensure that it behaves as expected. With the application started, you may want to use the command line curl (or your web browser, or the command wget or any other HTTP client):
