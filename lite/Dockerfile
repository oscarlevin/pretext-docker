FROM debian:bookworm-slim

RUN apt-get update \
&& apt-get install -y --no-install-recommends \
                    git \
                    wget \
                    npm \
                    python3 \
                    python3-pip \
                    python3-venv \
&& apt-get autoremove -y \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/* \
&& rm -rf /tmp/* /var/tmp/*

ENV VIRTUAL_ENV=/opt/venv
RUN python3 -m venv $VIRTUAL_ENV
ENV PATH="$VIRTUAL_ENV/bin:$PATH"

RUN apt-get update \
&& apt-get install -y --no-install-recommends \
                    python3-dev \
                    python3-louis \
                    libcairo2-dev \
                    librsvg2-bin \
                    gcc \
                    build-essential \
                    default-jre \
&& pip install pip --upgrade --no-cache-dir \
&& pip install pretext[homepage,prefigure] codechat-server --prefer-binary --no-cache-dir \
&& prefig init \
&& playwright install-deps \
&& playwright install chromium \
&& echo '/usr/lib/python3/dist-packages' > /usr/local/lib/python3.11/dist-packages/louis.pth \
&& echo '/usr/lib/python3/dist-packages' > /opt/venv/lib/python3.11/site-packages/louis.pth \
&& prefig init \
&& npm install @mermaid-js/mermaid-cli -g \
&& apt-get remove -y \
                    python3-dev \
                    libcairo2-dev \
                    gcc \
                    build-essential \
&& apt-get autoremove -y \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/* \
&& rm -rf /tmp/* /var/tmp/*

# make shell prompt pretty
RUN echo 'export PS1="\[\e[1;32m\]\u@\h:\[\e[1;34m\]\w \[\e[0m\]\$ "' >> ~/.bashrc