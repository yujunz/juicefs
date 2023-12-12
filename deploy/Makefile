# Modified from https://github.com/alexandrevilain/temporal-operator/blob/main/Makefile

# ENVTEST_K8S_VERSION refers to the version of kubebuilder assets to be downloaded by envtest binary.
ENVTEST_K8S_VERSION = 1.26

# Get the currently used golang install path (in GOPATH/bin, unless GOBIN is set)
ifeq (,$(shell go env GOBIN))
GOBIN=$(shell go env GOPATH)/bin
else
GOBIN=$(shell go env GOBIN)
endif

UNAME=$(shell uname -s)

VERSION ?= "$(shell cat VERSION)"

# Setting SHELL to bash allows bash commands to be executed by recipes.
# This is a requirement for 'setup-envtest.sh' in the test target.
# Options are set to exit when a recipe line exits non-zero or a piped command fails.
SHELL = /usr/bin/env bash -o pipefail
.SHELLFLAGS = -ec

.PHONY: all
all: build

##@ General

# The help target prints out all targets with their descriptions organized
# beneath their categories. The categories are represented by '##@' and the
# target descriptions by '##'. The awk commands is responsible for reading the
# entire set of makefiles included in this invocation, looking for lines of the
# file as xyz: ## something, and then pretty-format the target and help. Then,
# if there's a line with ##@ something, that gets pretty-printed as a category.
# More info on the usage of ANSI control characters for terminal formatting:
# https://en.wikipedia.org/wiki/ANSI_escape_code#SGR_parameters
# More info on the awk command:
# http://linuxcommand.org/lc3_adv_awk.php

.PHONY: help
help: ## Display this help.
	@awk 'BEGIN {FS = ":.*##"; printf "\nUsage:\n  make \033[36m<target>\033[0m\n"} /^[a-zA-Z_0-9-]+:.*?##/ { printf "  \033[36m%-15s\033[0m %s\n", $$1, $$2 } /^##@/ { printf "\n\033[1m%s\033[0m\n", substr($$0, 5) } ' $(MAKEFILE_LIST)

##@ Development

.PHONY: dev-cluster
dev-cluster: kind-with-registry
	$(KIND_WITH_REGISTRY)

.PHONY: clean-dev-cluster
clean-dev-cluster:
	kind delete clusters kind

##@ Build Dependencies

## Location to install dependencies to
LOCALBIN ?= $(shell pwd)/bin
$(LOCALBIN):
	mkdir -p $(LOCALBIN)

## Tool Binaries
KIND_WITH_REGISTRY ?= $(LOCALBIN)/kind-with-registry

## Tool Versions
KIND_WITH_REGISTRY_VERSION ?= 0.17.0

.PHONY: kind-with-registry
kind-with-registry: $(KIND_WITH_REGISTRY)
$(KIND_WITH_REGISTRY): $(LOCALBIN)
	curl -sLo $(KIND_WITH_REGISTRY) https://raw.githubusercontent.com/kubernetes-sigs/kind/v$(KIND_WITH_REGISTRY_VERSION)/site/static/examples/kind-with-registry.sh
	chmod +x $(KIND_WITH_REGISTRY)
