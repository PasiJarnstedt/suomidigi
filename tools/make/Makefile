.DEFAULT_GOAL := help

BUILD_TARGETS :=
CLEAN_FOLDERS := node_modules
COMPOSER_BIN := $(shell which composer || echo no)
COMPOSER_JSON_EXISTS := $(shell test -f composer.json && echo yes || echo no)
DOCKER_COMPOSE_BIN := $(shell which docker-compose || echo no)
DOCKER_COMPOSE_YML_EXISTS := $(shell test -f docker-compose.yml && echo yes || echo no)
DRUIDFI_TOOLS_MAKE_DIR := $(dir $(lastword $(MAKEFILE_LIST)))
ENV := dev
PACKAGE_JSON_EXISTS := $(shell test -f package.json && echo yes || echo no)
PHP_BIN := $(shell which php)
TEST_TARGETS := test-foobar
UNAME_S := $(shell uname -s)
# Shorten with https://git.io/ : https://raw.githubusercontent.com/druidfi/tools/master/update.sh
UPDATE_SCRIPT_URL := https://git.io/fh771
WEBROOT := public

# Detect additional tooling
AMAZEEIO_LEGACY := $(shell test -f .amazeeio.yml && echo yes || echo no)
AMAZEEIO_LAGOON := $(shell test -f .lagoon.yml && echo yes || echo no)
WODBY := $(shell test -f wodby.yml && echo yes || echo no)

ifeq ($(AMAZEEIO_LEGACY),yes)
	SYSTEM := AMAZEEIO
else ifeq ($(AMAZEEIO_LAGOON),yes)
	SYSTEM := AMAZEEIO
else ifeq ($(WODBY),yes)
	SYSTEM := WODBY
else
	SYSTEM := WHOKNOWS
endif

# Colors
NO_COLOR=\033[0m
GREEN=\033[0;32m
RED=\033[0;31m
YELLOW=\033[0;33m

# If docker-compose.yml exists
ifeq ($(DOCKER_COMPOSE_YML_EXISTS),yes)
	# If docker-compose does not exist (e.g. inside Docker container)
	ifeq ($(DOCKER_COMPOSE_BIN),no)
		RUN_ON := host
	else
		RUN_ON := docker
	endif
else
	RUN_ON := host
endif

PHONY += debug
debug: ## Show debug information
	@printf "${GREEN}Debug starts:${NO_COLOR}\n"
	$(call dbg,COMPOSER_BIN,${COMPOSER_BIN})
	$(call dbg,COMPOSER_JSON_EXISTS,${COMPOSER_JSON_EXISTS})
	$(call dbg,CLEAN_FOLDERS,${CLEAN_FOLDERS})
	$(call dbg,CLI_SERVICE,${CLI_SERVICE})
	$(call dbg,CLI_USER,${CLI_USER})
	$(call dbg,CLI_SHELL,${CLI_SHELL})
	$(call dbg,DOCKER_COMPOSE_BIN,${DOCKER_COMPOSE_BIN})
	$(call dbg,DOCKER_COMPOSE_YML_EXISTS,${DOCKER_COMPOSE_YML_EXISTS})
	$(call dbg,ENV,${ENV})
	$(call dbg,PHP_BIN,${PHP_BIN})
	$(call dbg,RUN_ON,${RUN_ON})
	$(call dbg,AMAZEEIO_LEGACY,${AMAZEEIO_LEGACY})
	$(call dbg,AMAZEEIO_LAGOON,${AMAZEEIO_LAGOON})
	$(call dbg,WODBY,${WODBY})
	$(call dbg,SYSTEM,${SYSTEM})
	$(call dbg,WEBROOT,${WEBROOT})
	$(call dbg,UNAME_S,${UNAME_S})
ifeq ($(RUN_ON),docker)
	@printf "${YELLOW}Assumption: We should run on Docker and not on host${NO_COLOR}\n"
else
	@printf "${YELLOW}Assumption: We should run on host and not on Docker${NO_COLOR}\n"
endif
	@printf "${GREEN}End of debug.${NO_COLOR}\n"

define dbg
	@printf "${GREEN}${1}:${NO_COLOR} ${2}\n"
endef

define step
	@printf "\n${YELLOW}${1}${NO_COLOR}\n\n"
endef

define warn
	@printf "\n${YELLOW}[warning]${NO_COLOR} ${1}\n\n"
endef

# Include druidfi/tools make files
include $(DRUIDFI_TOOLS_MAKE_DIR)include.mk
