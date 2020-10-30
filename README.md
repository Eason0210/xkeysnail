# xkeysnail Configuration
Configuration for xkeysnail with Emacs-like Keybinding.

## Install xkeysnail for offical repository.
### Arch Linux
```
yay -S xkeysnail
```
### From source
```bash
git clone --depth 1 https://github.com/mooz/xkeysnail.git
cd xkeysnail
sudo pip3 install --upgrade .
```
## download this repository

```bash
git clone https://github.com/Eason0210/xkeysnail.git
```

## Usage
```
sudo xkeysnail config.py
```
## Setting for automatic start
1. Edit the config file and replace `Your-terminal-app-here` with the window class of your terminal application.
(To get the window class name, run `xprop WM_CLASS` and click on the window of the terminal application)

2. Create a systemd service for xkeysnail to run automatically on the background:

```
cd /etc/systemd/system && sudo vim xkeysnail.service
```
3. Insert the following code to the service config and edit the path to the provided config file:
```
sudo vim /etc/systemd/system/xkeysnail.service
```

```
# https://qiita.com/samurai20000@github/items/2e1d779e806a7e8543d6
# https://github.com/mooz/xkeysnail/issues/12

[Unit]
Description=xkeysnail

[Service]
Environment=DISPLAY=:0
ExecStart=xkeysnail -q /home/aqua/.config/xkeysnail/config.py
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target
```
4. write `xhost +SI:localuser:root` to ~/.xsession , restart system.

5. Enable the xkeysnail service to auto start:
```
sudo systemctl enable xkeysnail
```
6. Start the xkeysnail service:
```
sudo systemctl start xkeysnail
```
7. If you want to edit config.py again, remember to restart service again.
```
sudo systemctl restart xkeysnail
```
## troubleshooting
To check if the xkeysnail service is running properly, run:
```
sudo systemctl status xkeysnail
```
If you encounter errors like `Xlib.error.DisplayConnectionError: Can't connect to display ":0.0": b'No protocol specified\n'`, make sure you have xhost package installed and try:
```
sudo xhost + && sudo systemctl restart xkeysnail
```
