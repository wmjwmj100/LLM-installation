# LLM-installation

# Running Ollama Locally on Android via Termux in AVD

This repository documents the process and findings of attempting to install and run Ollama with a Large Language Model (LLM) locally on an Android device using the Termux environment within an Android Virtual Device (AVD) managed by Android Studio.

**Project Goal:** To explore the feasibility of running Ollama and a specific LLM (`llama3.2:1b`) directly on an Android system simulated via AVD.

## Methodology

The approach involved:
1. Configuring a suitable Android Virtual Device (AVD) in Android Studio.
2. Installing the Termux terminal emulator within the AVD.
3. Installing Ollama within the Termux environment.
4. Attempting to run the Ollama server and load an LLM.

## 1. AVD Configuration

An AVD was configured in Android Studio with the following settings:

* **Device Profile:** Pixel 9 Pro
* **System Image:** Google APIs ARM 64 v8a System Image (API 36 - Android 16 'Baklava')
* **RAM:** **8 GB**.
* **VM Heap Size:** 256 MB
* **Preferred ABI:** `arm64-v8a`
* **CPU Cores:** 5
* **Internal Storage:** 128 GB

## 2. Termux Installation

Termux provides a Linux-like environment within Android.

* **Source:** It's recommended to install Termux from F-Droid or the [Termux GitHub releases page](https://github.com/termux/termux-app/releases).
* **APK Version:** The specific APK for the `arm64-v8a` architecture was downloaded and installed (`termux-app_v0.119.0-beta.2+apt-android-7-github-debug_arm64-v8a.apk`).

## 3. Ollama Installation in Termux

Two installation methods were attempted:

### Attempt 1: Official Install Script (Root Required)

The standard Linux installation script was run:

```bash
curl -fsSL [https://ollama.com/install.sh](https://ollama.com/install.sh) | sh
```

However, root access is generally not available on Google APIs/Play AVD images, making this script unsuitable for this environment.

### Attempt 2: Termux Package Manager (No Root Required)

Ollama was successfully installed using Termux's package manager via the Termux User Repository (TUR). This method does not require root.

```bash
# Update Termux packages
pkg update && pkg upgrade -y

# Install the TUR repository
pkg install tur-repo -y

# Install Ollama from TUR
pkg install ollama -y
```

## 4. Running Ollama Server

The Ollama server was started in a Termux session using:

```bash
ollama serve &
```

## 5. Attempting to Run an LLM (llama3.2:1b)

The next step was to load and run the target model in a new Termux session:

```bash
ollama run llama3.2:1b
```
