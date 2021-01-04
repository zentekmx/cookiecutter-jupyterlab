#
##
APPMAIL?="{{cookiecutter.author_email}}"
NOCLR=\x1b[0m
OKCLR=\x1b[32;01m
ERRCLR=\x1b[31;01m
WARNCLR=\x1b[33;01m
TEST_ARGS=
EXECUTABLES=docker pip python node
include .env
export $(shell sed 's/=.*//' .env)

define usage =
Build and development task automation tool for project"

Usage:
  make [task]
endef

## Built in tasks ##

#: help - Show Test info
help:
	$(info $(usage))
	@echo -e "\n  Available targets:"
	@egrep -o "^#: (.+)" [Mm]akefile  | sed 's/#: /    /'
	@echo "  Please report errors to ${APPMAIL}"

#: check - Check that system requirements are met
check:
	$(info Required: ${EXECUTABLES})
	$(foreach bin,$(EXECUTABLES),\
	    $(if $(shell command -v $(bin) 2> /dev/null),$(info Found `$(bin)`),$(error Please install `$(bin)`)))

# postgres - Start postgres container
postgres:
	@if [[ ! $$(docker ps -a | grep "${SLUG}-postgres") ]]; then \
		docker run -d --rm --name ${SLUG}-postgres -p ${DATABASE_PORT}:${DATABASE_PORT} -e POSTGRES_DB=${DATABASE_NAME} -e POSTGRES_USER=${DATABASE_USER} -e POSTGRES_PASSWORD=${DATABASE_PASSWORD} postgres:12-alpine; \
	else \
		echo "[${SLUG}-postgres] There is an existing postgres container name, I will use"; \
	fi

#: backend-start - Start backend services
backend-start: postgres
	@sleep 2
	@echo "Backend services started..."

#: backend-stop - Start backend services
backend-stop:
	if [[ $$(docker ps -a | grep "${SLUG}-postgres") ]]; then \
		docker stop ${SLUG}-postgres; \
	fi;
	@echo "Backend services stopped..."

#: jupyterlab - Run notebooks
jupyterlab:
	@jupyter lab --ip=0.0.0.0 --no-browser --notebook-dir ./notebooks

#: jupyterbook - Build notebooks
jupyterbook:
	@jupyter-book build ./notebooks

#: dbshell - Access database shell
dbshell:
ifeq (, $(shell which psql))
	$(info Required to install postgres package to use this function)
else
	@psql -h ${DATABASE_HOST} -p ${DATABASE_PORT} -U ${DATABASE_USER} -d ${DATABASE_NAME} -W
endif

#: ddl - Dump database ddl
ddl:
ifeq (, $(shell which pg_dump))
	$(info Required to install postgres package to use this function)
else
	@pg_dump "postgresql://${DATABASE_USER}:${DATABASE_PASSWORD}@${DATABASE_HOST}:${DATABASE_PORT}/${DATABASE_NAME}" -s > fixtures/ddl/ddl.sql
endif

#: schema - Dump database schema
schema:
ifeq (, $(shell which pg_dump))
	$(info Required to install postgres package to use this function)
else
	@pg_dump "postgresql://${DATABASE_USER}:${DATABASE_PASSWORD}@${DATABASE_HOST}:${DATABASE_PORT}/${DATABASE_NAME}" > fixtures/ddl/schema.sql
endif

# pipdep - Tweak pip dependencies before 20.3+
pipdep:
	@pip install pip==19.3.1  # for now ugly tweak to bypass any reference error

#: install - Install dependencies for current environment
install: pipdep
	pip install -r requirements.txt

#: install-jupyter - Install jupyter dependencies and extensions
install-extensions: pipdep
	jupyter labextension install jupyterlab-execute-time
	jupyter labextension install @jupyter-widgets/jupyterlab-manager
	jupyter labextension install @jupyterlab/toc
	jupyter labextension install @jupyterlab/debugger
	jupyter labextension install jupyterlab-jupytext
	jupyter labextension install @axlair/jupyterlab_vim
	jupyter labextension install @jupyter-widgets/jupyterlab-manager jupyter-leaflet
	jupyter labextension install jupyterlab-topbar-extension jupyterlab-system-monitor
	jupyter labextension install @bokeh/jupyter_bokeh
	jupyter labextension install jupyterlab-drawio
	jupyter labextension install @jupyterlab/commenting-extension
	jupyter labextension install @jupyterlab/google-drive

# clean - Remove build and python files
clean:
	@find . -name '*.py[cod~]' -exec rm -rf {} +

# clean-build - Remove build and python files
clean-dist:
	@rm -fr lib/
	@rm -fr build/
	@rm -fr dist/
	@rm -fr .tox/
	@rm -fr *.egg-info

# clean-containers - Remove docker files
clean-containers:
	@docker system prune --volumes

#: clean-all - Full clean
clean-all: clean clean-dist clean-containers

#: stop - Stop
stop: backend-stop

.PHONY: clean
