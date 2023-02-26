FROM ubuntu

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN apt-get update && \
    apt install curl wget git xz-utils lib32stdc++6 unzip default-jdk libxdamage-dev libfontconfig libglu1 libnss3-dev libxcomposite1 libxcursor1 libpulse0 libasound2 socat qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils -y

RUN	groupadd --gid $USER_GID $USERNAME && \
    useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME && \
    usermod -aG plugdev vscode && \
    adduser vscode libvirt && \
    adduser vscode kvm

#RUN chown vscode -R /dev/kvm

USER ${USERNAME}


WORKDIR /home/vscode

# Android SDK
RUN wget https://dl.google.com/android/repository/commandlinetools-linux-9477386_latest.zip && \
    mkdir android-sdk && \
    unzip commandlinetools-linux-9477386_latest.zip -d android-sdk/cmdline-tools && \
    rm commandlinetools-linux-9477386_latest.zip && \
    mv android-sdk/cmdline-tools/cmdline-tools android-sdk/cmdline-tools/latest

ENV ANDROID_HOME=/home/vscode/android-sdk
ENV ANDROID_SDK_ROOT=${ANDROID_HOME}
ENV PATH=${PATH}:${ANDROID_HOME}/cmdline-tools/latest/bin:${ANDROID_HOME}/platform-tools:${ANDROID_HOME}/emulator

RUN yes | sdkmanager --update && \
    yes | sdkmanager "platforms;android-29" "build-tools;28.0.3" "extras;google;m2repository" "extras;android;m2repository" && \
    yes | sdkmanager --licenses

# Flutter
RUN wget https://storage.googleapis.com/flutter_infra_release/releases/stable/linux/flutter_linux_3.3.0-stable.tar.xz && \
    tar xf flutter_linux_3.3.0-stable.tar.xz && \
    rm flutter_linux_3.3.0-stable.tar.xz

ENV PATH=/home/vscode/flutter/bin:${PATH}

RUN flutter precache