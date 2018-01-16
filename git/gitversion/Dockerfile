FROM mono:5.4

WORKDIR /usr/lib/GitVersion/
RUN mkdir /repo
VOLUME /repo

RUN apt-get update && apt-get  -y --no-install-recommends --allow-unauthenticated install unzip

ADD https://github.com/GitTools/GitVersion/releases/download/v3.6.5/GitVersion_3.6.5.zip /tmp/GitVersion.zip
RUN unzip -d /usr/lib/GitVersion/ /tmp/GitVersion.zip && \
    rm /tmp/GitVersion.zip && \
    sed -i 's|lib/linux/x86_64|/usr/lib/GitVersion/lib/linux/x86_64|g' /usr/lib/GitVersion/LibGit2Sharp.dll.config

ENTRYPOINT ["mono", "/usr/lib/GitVersion/GitVersion.exe", "/repo"]