FROM ubuntu

ENV gradle_version=4.10.2
ENV gradle_install_path=/opt/gradle-${gradle_version}

RUN apt-get -y update
RUN apt-get -y upgrade
RUN apt-get -y install wget unzip

RUN mkdir /tmp/kotlin-native-bootstrap
WORKDIR /tmp/kotlin-native-bootstrap

# Install JDK 8:
RUN apt-get -y install openjdk-8-jdk

# Install Gradle:
RUN wget https://services.gradle.org/distributions/gradle-${gradle_version}-bin.zip
RUN unzip ./gradle-*.zip
RUN mv ./gradle-${gradle_version} ${gradle_install_path}

# Install Kotlin/Native through the bootstrap Gradle project:
COPY ./build.gradle ./
RUN ${gradle_install_path}/bin/gradle model

RUN echo "export PATH=\$PATH:`ls -1d /root/.konan/kotlin-native-*/ | head -n 1`bin" > /root/.bashrc

RUN rm -rf /tmp/*
WORKDIR /root

ENTRYPOINT /bin/bash
