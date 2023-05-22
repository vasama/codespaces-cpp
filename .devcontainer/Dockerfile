FROM mcr.microsoft.com/devcontainers/base:ubuntu
USER root

# Install Kitware apt repository for latest CMake.
RUN wget -O - https://apt.kitware.com/kitware-archive.sh 2>/dev/null | sh && \
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
