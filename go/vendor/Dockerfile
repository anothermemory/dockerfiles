FROM anothermemory/go-base

ADD git-vendor/glide.* /am/
RUN cd /am && \
    glide install --force --v && \
    mv /am/vendor/* /go/src && \
    cd /go/src && \
    RUN rm -rf ./am