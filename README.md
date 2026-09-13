# DLNA-on-Windows

This repository explains how to use Windows as a DLNA media server on your
local network.

## Supported Windows versions

- Windows 10
- Windows 11

## What you need

- A Windows PC connected to the same local network as your TV, console, phone,
  or other DLNA client
- Media files stored on the Windows PC
- Network discovery enabled

## How to run DLNA on Windows

Windows can share media over DLNA by using the built-in media streaming
features.

1. Open **Control Panel**.
2. Go to **Network and Internet** -> **Network and Sharing Center**.
3. Click **Media streaming options**.
4. Click **Turn on media streaming**.
5. Give your media library a name if you want.
6. Make sure your DLNA client devices are allowed.
7. Click **OK** to save the settings.

## Add media to the library

To make your files available to DLNA clients:

1. Open **Windows Media Player Legacy** from the Start menu.
2. Press **Alt** if the menu bar is hidden.
3. Select **Organize** -> **Manage libraries**.
4. Choose **Music**, **Videos**, or **Pictures**.
5. Click **Add** and select the folder that contains the media you want to
   share.
6. Click **Include folder**, then **OK**.
7. Wait for Windows Media Player to index the new files.

After that, compatible devices on the same network should be able to discover
your Windows PC and browse the shared media.

## Troubleshooting

- Make sure both devices are on the same network.
- Set your network profile to **Private**.
- Allow Windows Media Player or media streaming through the Windows Firewall.
- Restart the DLNA client device if it does not appear immediately.
- Reopen **Media streaming options** to confirm streaming is still enabled.

## Notes

This repository currently contains setup instructions only. It does not include
a custom DLNA server application or Windows service.
