FROM python:3-slim

LABEL description="Scanning APK file for URIs, endpoints & secrets."
LABEL repository="https://github.com/dwisiswant0/apkleaks"
LABEL maintainer="dwisiswant0"

WORKDIR /app

COPY requirements.txt .
RUN python -m ensurepip
RUN pip install -r requirements.txt

# Install necessary dependencies and OpenJDK from AdoptOpenJDK
RUN apt-get update && \
    apt-get install -y wget unzip && \
    wget https://github.com/AdoptOpenJDK/openjdk11-binaries/releases/download/jdk-11.0.11+9/OpenJDK11U-jdk_x64_linux_hotspot_11.0.11_9.tar.gz && \
    tar xzf OpenJDK11U-jdk_x64_linux_hotspot_11.0.11_9.tar.gz -C /opt && \
    ln -s /opt/jdk-11.0.11+9 /opt/jdk && \
    ln -s /opt/jdk/bin/java /usr/local/bin/java && \
    rm OpenJDK11U-jdk_x64_linux_hotspot_11.0.11_9.tar.gz && \
    wget https://github.com/skylot/jadx/releases/download/v1.4.5/jadx-1.4.5.zip && \
    unzip jadx-1.4.5.zip -d /opt/jadx && \
    ln -s /opt/jadx/bin/jadx /usr/local/bin/jadx && \
    ln -s /opt/jadx/bin/jadx-gui /usr/local/bin/jadx-gui && \
    rm jadx-1.4.5.zip

COPY . .

ENTRYPOINT ["python", "/app/apkleaks.py"]
