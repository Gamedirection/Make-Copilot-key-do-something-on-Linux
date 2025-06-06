# Guide to Enhancing HP ProBook 460 G11 on Linux with Copilot Key

This guide provides step-by-step instructions to optimize your HP ProBook 460 G11, or similar models, by configuring the Copilot key on Linux. It covers the installation of essential software, remapping of keys, and setting up a hotkey for enhanced productivity.

Note: I am a hobbyist Linux User but would like to share this method both as a way for my self to repeat this in the inevitable future that I will need this guide or for any folks like myself who are currently struggling to find the solution.
Any suggestions to improve the guide is welcomed, esp for other operating systems and configurations. The Co-pilot key bugs me so much.

Please Star + Share this guide with your favorite discord groups, the folks who want this may not even know it yet.

## Prerequisites

- An HP ProBook 460 G11 or a similar model
- Linux operating system (Ubuntu 25 is what I am using in this example)

## Preparations

Before proceeding with the installations, ensure your system is up-to-date:

```bash
sudo apt update
sudo apt install git
sudo apt install curl
sudo apt install cmake libudev-dev git
```

## Install Albert

Albert is a versatile application launcher that will enhance your machine's functionality. For more distros:
https://software.opensuse.org/download/package.iframe?project=home:manuelschneid3r&package=albert&acolor=00cccc&hcolor=00aaaa&locale=en

### For Ubuntu 25 or similar builds:

1. Add the repository:
   ```bash
   echo 'deb http://download.opensuse.org/repositories/home:/manuelschneid3r/xUbuntu_25.04/ /' | sudo tee /etc/apt/sources.list.d/home:manuelschneid3r.list
   ```
2. Add the GPG key:
   ```bash
   curl -fsSL https://download.opensuse.org/repositories/home:manuelschneid3r/xUbuntu_25.04/Release.key | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/home_manuelschneid3r.gpg > /dev/null
   ```
3. Update and install Albert:
   ```bash
   sudo apt update
   sudo apt install albert
   ```

## Install "Keyd"

Keyd is a key remapping daemon that will help you configure your keyboard to use the Copilot key efficiently.

1. Clone the Keyd repository:
   ```bash
   git clone https://github.com/rvaiya/keyd
   cd keyd
   ```
2. Build and install Keyd:
   ```bash
   make && sudo make install
   sudo apt install keyd
   ```
3. Enable and start the Keyd service:
   ```bash
   sudo systemctl enable keyd
   sudo systemctl start keyd
   ```

## Check Copilot Key Functionality

To verify what your Copilot key is doing, execute:

```bash
sudo keyd -m
```

### Expected Output

Your input should resemble the following:

```plaintext
input-remapper AT Translated Set 2 keyboard forwarded 0001:0001:39128cca leftmeta down
input-remapper AT Translated Set 2 keyboard forwarded 0001:0001:39128cca leftshift down
input-remapper AT Translated Set 2 keyboard forwarded 0001:0001:39128cca f23 down
input-remapper AT Translated Set 2 keyboard forwarded 0001:0001:39128cca leftmeta up
input-remapper AT Translated Set 2 keyboard forwarded 0001:0001:39128cca leftshift up
input-remapper AT Translated Set 2 keyboard forwarded 0001:0001:39128cca f23 up
```

## Update Configuration with Macro

Edit the default Keyd configuration file:

```bash
sudo nano /etc/keyd/default.conf
```

### Add the following lines to the configuration file:

```plaintext
[ids]
*
[main]
# Remap Copilot key (LeftMeta+LeftShift+F23) to Ctrl+Space
leftmeta+leftshift+f23 = C-space
```

## Reload and Test Configuration

To apply and verify the configuration changes, execute:

```bash
sudo keyd reload
sudo keyd -m
```

### Expected Output

The output should look like this:

```plaintext
keyd virtual keyboard 0fac:0ade:bea394c0 leftcontrol down
keyd virtual keyboard 0fac:0ade:bea394c0 space down
keyd virtual keyboard 0fac:0ade:bea394c0 space up
keyd virtual keyboard 0fac:0ade:bea394c0 leftcontrol up
```

## Set Hot Key

Set up a hotkey in the Albert menu to utilize the new mapping. Choose either `Ctrl+Space` with the standard control and space keys, or utilize the newly configured Copilot key.

This comprehensive guide should have helped you set up the key remapping and Albert app launcher on your HP ProBook 460 G11 for optimal productivity on Linux. Enjoy the enhanced functionality!

If you are on Ubuntu you may need to set the shortcut to launch albert like this
```plaintext
Name: albert
Command: albert toggle
Hotkey: CTRL+Space
```
![image](https://github.com/user-attachments/assets/dd9c7d44-5459-420e-b340-0479ae151009)

