FROM amazonlinux:latest

RUN yum install -y \
    rpmdevtools \
    wget \
    yum-utils

WORKDIR /tmp

# Download wkhtmltopdf and its dependencies. Then extract all rpm files.
ENV WKHTMLTOPDF_BIN="wkhtmltopdf.rpm"
RUN wget -O $WKHTMLTOPDF_BIN https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6.1-3/wkhtmltox-0.12.6.1-3.almalinux8.x86_64.rpm \
    && yum install -y --downloadonly --downloaddir=/tmp $WKHTMLTOPDF_BIN \
    && yumdownloader --archlist=x86_64 \
    bzip2-libs \
    expat \
    libuuid \
    && rpmdev-extract *rpm

WORKDIR /layer

# Copy wkhtmltopdf binary and dependency libraries for packaging
RUN mkdir -p {bin,lib} \
    && cp /tmp/wkhtml*/usr/local/bin/* bin \
    && cp /tmp/*/usr/lib64/* lib || :

# Zip files
ENV LAYER_ZIP="layer.zip"
RUN zip -r $LAYER_ZIP bin lib \
    && mv $LAYER_ZIP /