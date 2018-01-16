FROM ubuntu:16.04

# moviong the timezone setting at the top, as this may be the most infrequent change in this file
#RUN ln -sfn /usr/share/zoneinfo/GMT /etc/localtime

# Following current install guide from
# http://www.mono-project.com/download/#download-lin on 2017-12-08
# regarding to the repository sources
RUN echo "deb http://download.mono-project.com/repo/ubuntu xenial main" |\
    tee /etc/apt/sources.list.d/mono-official.list

# This will do:
# * Accept the repository key
# * Get the current package inventory state
# * Install given packages only with required dependencies
# * Cleanup to reduce Docker image size
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF &&\
    apt-get update &&\
    apt-get  -y --no-install-recommends install libcurl3 tzdata unzip curl git-all mono-complete &&\
    apt-get -yqq clean &&\
    rm -rf /var/lib/apt/lists/* /tmp/*



WORKDIR /usr/lib/GitVersion/
ADD https://github.com/GitTools/GitVersion/releases/download/v3.6.5/GitVersion_3.6.5.zip /tmp/GitVersion.zip
RUN unzip -d /usr/lib/GitVersion/ /tmp/GitVersion.zip && rm /tmp/GitVersion.zip

# Libgit2 can't resolve relative paths, patch to absolute path
RUN sed -i 's|lib/linux/x86_64|/usr/lib/GitVersion/lib/linux/x86_64|g' /usr/lib/GitVersion/LibGit2Sharp.dll.config

RUN mkdir /repo
VOLUME /repo

ENTRYPOINT ["mono", "/usr/lib/GitVersion/GitVersion.exe", "/repo"]
