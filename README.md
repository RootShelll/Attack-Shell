# Attack Shell (Ani-Shell)

![Attack Shell Logo](https://r00t-shell.com/wp-content/uploads/2025/02/Attack-Shell-Ani-Shell.png)

**Version:** v1.0-Alpine (Last updated: February 24, 2017)

**Warning:** This software is intended for demonstration and educational purposes only. Ensure you have the necessary permissions before use, and use it at your own risk.

## Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Installation and Configuration](#installation-and-configuration)
  - [Running with Docker](#running-with-docker)
  - [Configuring with a Custom `php.ini` File](#configuring-with-a-custom-phpini-file)
- [Customization and Security Settings](#customization-and-security-settings)
- [Usage Guide](#usage-guide)
  - [Accessing the Shell](#accessing-the-shell)
  - [Interface Overview](#interface-overview)
  - [Using Advanced Features](#using-advanced-features)
  - [Troubleshooting and Support](#troubleshooting-and-support)
- [Conclusion](#conclusion)

## Introduction

Attack Shell, also known as Ani-Shell, is a powerful PHP shell equipped with unique features such as mass mailer, web server fuzzer, dosser, back connect, bind shell, and auto rooter. It is designed with open coding standards, making customization straightforward; ideal for both beginners and advanced users interested in cybersecurity and penetration testing.

Whether you're learning the basics of security for the first time or conducting comprehensive tests in your environment, this tool offers a flexible platform for education and experimentation.

## Features

- Interactive PHP shell
- Intelligent file manager
- Auto rooter for privilege escalation
- PHP code obfuscation
- Mass mailer (for responsible use)
- Web server fuzzer to identify vulnerabilities
- Dosser for simulating DoS attacks
- Bind shell and back connect features
- Customizable security settings (lock mode, anti-crawler)
- Email traceback and notifications
- Mass code injector for adding or modifying code
- MD5 hash cracker
- Python bind-shell integration

## Installation and Configuration

### Running with Docker

To quickly set up Attack Shell, you can use Docker to run it in a local container. Open your terminal and execute the following command:

```bash
docker run -d -p 80:80 --name attack-shell R00t-Shelll/attack-shell
```


To find the container's IP address, run:

```bash
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' attack-shell
```

### Configuring with a Custom `php.ini` File

If you require custom PHP settings, you can update the Dockerfile as follows:

```dockerfile
FROM k0st/alpine-apache-php

LABEL maintainer "your-email@example.com"

# Set your timezone (e.g., Europe/Istanbul)
ENV TZ=Europe/Istanbul

RUN apk add --update --virtual .build-deps tzdata && \
  ln -snf /usr/share/zoneinfo/${TZ} /etc/localtime && \
  echo "${TZ}" > /etc/timezone && \
  apk del .build-deps

COPY config/php.ini /usr/local/etc/php/
COPY . /var/www/html
```

**Note:** Replace `your-email@example.com` with your email address and ensure the `php.ini` file is correctly configured.

## Customization and Security Settings

Attack Shell comes with the following default settings, which you can modify to suit your needs:

1. **Default Login Credentials:** Username: `admin` and Password: `R00t`. It's crucial to change these immediately after installation.
2. **Lock Mode:** Enabled by default to prevent unauthorized access. Do not disable unless you are certain your security measures are adequate.
3. **Anti-Crawler Feature:** Disabled by default. Enable it to block automated bots from accessing the shell.
4. **Customizable Greeting Messages:** Modify the `greetings` variable to personalize the shell's welcome message.

## Usage Guide

### Accessing the Shell

After installation, open your browser and navigate to the IP address or domain where the container is hosted. Log in using the default credentials:

**Warning:** Immediately change the default login credentials to secure your system.

### Interface Overview

Upon logging in, you'll be presented with an intuitive interface that provides access to all features, including the file manager, command execution panel, and various tools.

### Using Advanced Features

- **Mass Mailer:** Send bulk emails responsibly. Ensure you have permission to contact recipients.
- **Web Server Fuzzer:** Test your server for common vulnerabilities.
- **Dosser:** Simulate Denial of Service attacks in a controlled environment.
- **Auto Rooter:** Attempt privilege escalation where applicable.
- **Bind Shell/Back Connect:** Establish reverse or bind shell connections for remote access.

**Note:** Use these features ethically and only on systems you own or have explicit permission to test.

### Troubleshooting and Support

If you encounter issues:

- Verify that your server meets the necessary requirements.
- Ensure all configurations are correct.
- Consult the [official GitHub repository](https://github.com/RootShelll) for updates and community support.

## Conclusion

Attack Shell offers a comprehensive suite of tools for those interested in cybersecurity and penetration testing. Always use it responsibly, ethically, and within the bounds of the law. 
