# DLNA-on-Windows
DLNA on Windows

Install WSL 2 + Ubuntu
Install net-tools
Create the Windows-user-level %USERPROFILE%\.wslconfig with mirrored networking
Access D:\Movies from Linux as /mnt/d/Movies
Optionally create ~/Movies as a convenient Linux path pointing to D:\Movies

Microsoft recommends wsl --install for current Windows versions.

1. Install WSL and Ubuntu

Open PowerShell as Administrator and run:

```bash
wsl --install -d Ubuntu
```


## Restart Windows when prompted.

After reboot, Ubuntu should open automatically. Create your Linux username and password when asked.

Then, from PowerShell, verify:

```bash
wsl --status
wsl --version
wsl --list --verbose
```

### You want Ubuntu to show VERSION 2.

If it shows version 1, run:

wsl --set-version Ubuntu 2

wsl --set-default-version 2


## 2. Update Ubuntu and install net-tools

Open Ubuntu/WSL and run:

```bash 
sudo apt update
sudo apt upgrade -y
sudo apt install -y net-tools
```

You can verify it with:

```bash
ifconfig
netstat -rn
route -n
```

## 3. Create .wslconfig with mirrored networking

Important distinction:

.wslconfig → global WSL 2 configuration, stored in your Windows user profile
wsl.conf → configuration inside a specific Linux distribution at /etc/wsl.conf

For mirrored networking, you want .wslconfig. Microsoft documents networkingMode=mirrored under the [wsl2] section. It requires Windows 11 22H2 or newer.

In PowerShell, run:
```bash
notepad $env:USERPROFILE\.wslconfig

```

Put this into the file 

```bash
[wsl2]
networkingMode=mirrored
```


The actual file will be:

C:\Users\<YourWindowsUsername>\.wslconfig


## 4. Restart WSL so the configuration takes effect

From PowerShell:

```bash

wsl --shutdown

wsl -d Ubuntu

```

## 5. Install minidlna

```bash

sudo apt update
sudo apt install -y minidlna

```

### Configure it for D:\Movies

```bash
sudo cp /etc/minidlna.conf /etc/minidlna.conf.backup
```

```bash
sudo nano /etc/minidlna.conf
```

after that edit media_dir section

```bash

media_dir=V,/mnt/d/Movies
friendly_name=WSL Movie Server
inotify=yes
```

Test minidlna can read the directory

```bash

sudo -u minidlna find /mnt/d/Movies -maxdepth 2 -type f | head -20

```

4. Rebuild the MiniDLNA database

Run:

```bash
sudo minidlnad -R
```

```bash
sudo service minidlna start
```

```bash
sudo service minidlna status
```

## Try from the browser if the miniDLNA server is going to work

http://<WSL-IP>:8200
