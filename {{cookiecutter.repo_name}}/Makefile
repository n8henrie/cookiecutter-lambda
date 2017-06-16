GREP := $(shell command -v ggrep || command -v grep)
SED := $(shell command -v gsed || command -v sed)

help:
	@$(GREP) --only-matching --word-regexp '^[^[:space:].]*:' Makefile | SED 's|:[[:space:]]*||'

deps:
	mkdir -p deps
	pip3 install --upgrade --target=deps n8scripts

publish: deps
	rm -f index.zip 
	cd deps && zip --recurse-paths ../index.zip ../*.py *
	aws lambda update-function-code --function-name {{ cookiecutter.func_name }} --zip-file fileb://index.zip

clean-deps:
	rm -rf deps/*

.PHONY: help clean-deps
