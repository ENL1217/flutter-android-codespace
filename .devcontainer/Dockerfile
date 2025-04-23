##########################################
# Stage 1 – 下載並安裝 Flutter SDK
##########################################
FROM ubuntu:22.04 AS flutter-setup

RUN apt-get update && apt-get install -y \
    git curl unzip wget xz-utils

# 下載 stable 版 Flutter
RUN git clone https://github.com/flutter/flutter.git -b stable /flutter
ENV PATH="/flutter/bin:$PATH"

# 預先執行 doctor（產生初始快取，後面建置較快）
RUN flutter doctor -v



##########################################
# Stage 2 – 最終執行環境
##########################################
FROM ubuntu:22.04

# 安裝最小依賴：JDK、編譯工具、OpenGL 基本庫
RUN apt-get update && apt-get install -y --no-install-recommends \
    openjdk-11-jdk \
    build-essential \
    libgl1-mesa-dev \
    git curl unzip wget \
    && rm -rf /var/lib/apt/lists/*

# 複製 Flutter SDK 進來
COPY --from=flutter-setup /flutter /flutter
ENV PATH="/flutter/bin:$PATH"

# ---（可選）Android SDK ----
ENV ANDROID_HOME=/usr/local/android-sdk
ENV PATH="$PATH:$ANDROID_HOME/cmdline-tools/latest/bin:$ANDROID_HOME/platform-tools"

# 你若要完整 Android SDK，可在這裡加上下載腳本或 sdkmanager 指令
