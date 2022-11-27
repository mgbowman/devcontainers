FROM node

# https://github.com/go-task/task
ARG TASK_VERSION
ARG TASK_SHA256

# https://github.com/devcontainers/cli
RUN --mount=type=cache,mode=0755,target=/var/cache/apt \
		export DEBIAN_FRONTEND=noninteractive \
	&& apt-get update \
	&& apt-get install -y --no-install-recommends \
                build-essential \
                ca-certificates \
                curl \
                gnupg \
                lsb-release \
                python-is-python3 \
                python3 \
	&& mkdir -p /etc/apt/keyrings \
        && curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg \
        && echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
                https://download.docker.com/linux/debian \
                $(lsb_release -cs) stable" | \
                tee /etc/apt/sources.list.d/docker.list > /dev/null \
        && apt-get update \
        && apt-get install -y --no-install-recommends \
                docker-ce-cli \
        && apt-get autoremove \
        && apt-get clean -y \
        && rm -rf /var/lib/apt/lists/* \
        && curl -fsSL "https://github.com/go-task/task/releases/download/v${TASK_VERSION}/task_linux_amd64.tar.gz" > /usr/local/bin/task.tar.gz \
        && echo "${TASK_SHA256}  /usr/local/bin/task.tar.gz" | sha256sum -c \
        && tar -C /usr/local/bin -zxf /usr/local/bin/task.tar.gz task \
        && rm -f /usr/local/bin/task.tar.gz \
        && chown root:root /usr/local/bin/task \
        && chmod 0755 /usr/local/bin/task \
	&& npm install -g npm \
 	&& npm install -g @devcontainers/cli
