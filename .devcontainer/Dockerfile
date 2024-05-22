# Copyright (C) VinFast
# All rights reserved
# Proprietary and confidential

# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.238.0/containers/ubuntu/.devcontainer/base.Dockerfile

# [Choice] Ubuntu version: ubuntu-24.04, ubuntu-22.04, ubuntu-20.04, ubuntu-18.04
ARG VARIANT="ubuntu-24.04"
FROM mcr.microsoft.com/vscode/devcontainers/base:${VARIANT}

# Remove conflicting "ubuntu" user with GUID 1000
# Reference: https://github.com/devcontainers/images/issues/1056#issue-2286172610
RUN userdel -r ubuntu || true

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
# Sphinx and sphinx-needs are Python 3 pip modules.
    && apt-get -y install --no-install-recommends python3 python3-pip \
# PlantUML together with Graphviz create UML diagrams from a textual description and are required by sphinxcontrib-plantuml.
    plantuml graphviz \
# The build uses the following elements.
    cmake clang gcc g++ gdb googletest ninja-build \
# Latest stable clang tools for formatting and linting the code
    clang-format \
    clang-tidy \
# valgrind identifies memory leaks and accesses to uninitialized variables.
    valgrind \
# Doxygen for documenting code with breathe
    doxygen \
# autopep8 nicely formats Python code.
    python3-autopep8

# This setting is required for the credentials to be correctly retrieved inside the development container.
# Reference: https://github.com/microsoft/vscode/issues/121420#issuecomment-988400262
RUN git config --global credential.useHttpPath true
RUN git config --global --add safe.directory /workspace

# Enable the git command / branch completion.
RUN echo "source /usr/share/bash-completion/completions/git" >> /etc/bash.bashrc
