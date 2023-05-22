FROM mcr.microsoft.com/devcontainers/base:ubuntu
USER root

# Install Kitware apt repository for latest CMake.
RUN apt-get update && \
    apt-get install -y software-properties-common lsb-release && \
    wget -O - https://apt.kitware.com/keys/kitware-archive-latest.asc 2>/dev/null | \
        gpg --dearmor - | \
        tee /etc/apt/trusted.gpg.d/kitware.gpg >/dev/null && \
    apt-add-repository "deb https://apt.kitware.com/ubuntu/ $(lsb_release -cs) main" && \
    apt-get update && \
    apt-get install -y kitware-archive-keyring && \
    rm /etc/apt/trusted.gpg.d/kitware.gpg && \
    apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/*

# Install development tools.
RUN apt-get update && \
    apt-get install -y \
        build-essential \
        clang \
        cmake \
        cppcheck \
        gdb \
        lldb \
        llvm \
        valgrind \
        && \
    apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/*

COPY requirements.txt /tmp/pip-tmp/requirements.txt
RUN python3 -m pip install --upgrade pip setuptools && \
    pip3 install --no-input --no-cache-dir -r /tmp/pip-tmp/requirements.txt && \
    rm /tmp/pip-tmp/requirements.txt
