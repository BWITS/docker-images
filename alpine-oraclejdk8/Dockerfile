FROM frolvlad/alpine-glibc:alpine-3.5_glibc-2.25 

# The purpose of this Dockerfile is to create a tag that specifies both versions of the OS and the JDK.
# Unfortunately there's none available on Docker HUB.
# This is taken from https://hub.docker.com/r/frolvlad/alpine-oraclejdk8/~/dockerfile/
# If the author of https://hub.docker.com/r/frolvlad/alpine-oraclejdk8 adds proper tags, we could ditch this one.

ENV JAVA_VERSION=8 \
    JAVA_UPDATE=121 \
    JAVA_BUILD=13 \
    JAVA_PATH=e9e7ea248e2c4826b92b3f075a80e441 \
    JAVA_HOME="/usr/lib/jvm/default-jvm"

RUN apk add --no-cache --virtual=build-dependencies wget ca-certificates unzip && \
    cd "/tmp" && \
    wget --header "Cookie: oraclelicense=accept-securebackup-cookie;" \
        "http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION}u${JAVA_UPDATE}-b${JAVA_BUILD}/${JAVA_PATH}/jdk-${JAVA_VERSION}u${JAVA_UPDATE}-linux-x64.tar.gz" && \
    tar -xzf "jdk-${JAVA_VERSION}u${JAVA_UPDATE}-linux-x64.tar.gz" && \
    mkdir -p "/usr/lib/jvm" && \
    mv "/tmp/jdk1.${JAVA_VERSION}.0_${JAVA_UPDATE}" "/usr/lib/jvm/java-${JAVA_VERSION}-oracle" && \
    ln -s "java-${JAVA_VERSION}-oracle" "$JAVA_HOME" && \
    ln -s "$JAVA_HOME/bin/"* "/usr/bin/" && \
    rm -rf "$JAVA_HOME/"*src.zip && \
    wget --header "Cookie: oraclelicense=accept-securebackup-cookie;" \
        "http://download.oracle.com/otn-pub/java/jce/${JAVA_VERSION}/jce_policy-${JAVA_VERSION}.zip" && \
    unzip -jo -d "${JAVA_HOME}/jre/lib/security" "jce_policy-${JAVA_VERSION}.zip" && \
    rm "${JAVA_HOME}/jre/lib/security/README.txt" && \
    apk del build-dependencies && \
    rm "/tmp/"*

