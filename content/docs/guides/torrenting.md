---
title: Torrenting + VPN Guide
description: Complete guide to safe torrenting with VPN setup, binding, and testing procedures
weight: 1
---

## Background Information

### Torrenting Risks
- Torrenting is very different from direct downloads or streaming sites in that it operates on a peer-to-peer file sharing network. 
- In order to be able to share with others peers on the network, your IP address becomes visible to anyone in the torrent swarm.
- In certain countries (Germany, USA, etc) there are specialized law firms that monitor and collect IP addresses participating in certain torrent swarms. These firms will send DMCA letters to the ISP who is responsible for that address, then the ISP will forward those letters to you. In Germany this can include demands for hundreds of euros in fines or face legal action. In the USA, this can result in temporary disruptions to your network connection, and eventually your ISP may cancel your service entirely.

### VPN
- Because of the risks mentioned above, a VPN becomes necessary to hide your IP address when torrenting in those countries.
- A VPN routes your network traffic through a remote server, serving as a middle-man and hiding your home IP address.
- When you torrent with a VPN, the IP address exposed in the torrent swarm is that of the VPN server, not your home IP. Because of this, torrent activity cannot be traced back to you, and therefore you will not receive DMCA letters.

### Proper VPN Setup
- Simply using a VPN is NOT sufficient to fully hide your IP address.
- There are many failure mechanisms that could leak your IP even when using a VPN.
	- User error (forgot to turn VPN on, closed VPN before exiting torrent application).
	- Momentary loss in VPN connection (VPN provider disconnect, local network problems, computer shutdown).
- ANY loss in VPN connection, no matter how short (fractions of a second) is enough to leak your home IP and get you a DMCA letter.
- Because of this, **"binding" your VPN to your torrent client is required in order to completely eliminate the risk of IP leaks**.
- WARNING: Kill Switches
	- Kill switches are NOT sufficient to protect you. They are reactionary and any delay in killing the application/connection will lead to your IP leaking. 
	- Kill switches are not the same as binding your VPN. 
	- Kill switches will fail eventually and you will get caught.

### Choosing a VPN Provider
- There are literally hundreds of VPN providers to choose from, how do you know which to pick?
- Many factors come into consideration: price, speed, security (no-logs policy, based in country friendly to piracy), features (port forwarding, split tunneling).
- Right now my recommendation for a VPN provider for torrenting would be [**Proton Premium**](https://protonvpn.com/), but feel free to use your provider of choice (this guide will use Proton Premium as an example). [**FMHY's VPN list**](https://fmhy.net/privacy#vpn) offers some alternatives.
- Free VPN's are not recommended for torrenting. Proton's free plan DOES NOT SUPPORT torrenting.

---

## Windows

### Installation
- Choose your VPN provider and install their application and sign in (download link for [Proton](https://protonvpn.com/download)).
- Choose a VPN server to connect to in the VPN application.
	- Pick the closest server with the best ping. It is not necessary to choose a server in another country.
	- If your provider has P2P specific servers (like Proton), then be sure to choose one of those.
- Install your torrent client ([**qBittorrent**](https://www.qbittorrent.org/) highly recommended and will be used throughout this guide).

### Bind Your VPN to Your Torrent Client (critical)
- In qBittorrent, go to Tools > Options > Advanced
- Find the Network Interface setting and change it from "Any" to the option that matches your VPN.
	- For Proton the option will be either "ProtonVPN" or "ProtonVPN TUN" depending on whether you are using OpenVPN or Wireguard (per [THIS](https://protonvpn.com/support/bittorrent-vpn) guide).
	- If you aren't sure which interface is correct, go to Control Panel > Network and Internet > Network Connections. Find the adapter that your VPN is using here and choose that name in qBit.
	- If you still cannot determine which option is correct, try toggling your VPN off and on to see which option disappears / reappears from the qBit list.
- Restart qBittorrent.

### Test Your VPN Binding (optional but recommended)
- Pause or remove all torrents currently in your torrent client
- Turn on your VPN
- Disable any kill switch you may use, we don't want to test the kill switch, we want to test the binding
- Go to ipleak.net
- Click "activate" button under "torrent address detection"
- Click "add this magnet link"
- Torrent will be added to your torrent client
- You should see only your VPN IP address in the browser in the "torrent address detection" section (ignore all the other sections, they don't matter for torrenting)
- NOW, SHUT OFF YOUR VPN (leave your torrent client running)
- You should still see only your VPN IP in the torrent detection list (or nothing at all)
- IF AT ANY POINT YOU SEE YOUR HOME IP ADDRESS (in the "torrent adress detection" section), SOMETHING IS WRONG. Go back and retry VPN binding steps / choose different network adapter.
- Additional testing (optional): go to [**FossTorrents**](https://fosstorrents.com/distributions/arcolinux/), click the magnet link for ArcoNet (popular Linux Distro), let the torrent start and then verify that your download speed in your torrent client drops to zero when you disconnect from your VPN (will take a few minutes to drop all the way to zero).

### Exclude Problematic File Extensions (optional but recommended)
- In qBittorrent, go to Tools > Options > Downloads > Excluded File Names
	- In the excluded file names list in the qB settings add the extensions you want to exclude, ONE EXTENSION PER LINE. Put an asterisk (wildcard) before each extension. I would recommend blocking AT LEAST the following three extensions:
```
*.lnk
*.scr
*.arj
```

### Set up Port Forwarding (optional but recommended)
- Enable port forwarding in your VPN app and find your forwarded port number in your VPN client (Proton guide shown [**HERE**](https://protonvpn.com/support/port-forwarding#windows))
- In qBittorrent, go to Tools > Options > Connections (Proton guide shown [**HERE**](https://protonvpn.com/support/port-forwarding#qbittorrent)).
- Uncheck the "Use UPnP / NAT-PMP port forwarding from my router" option.
- In the "Port used for incoming connections" field, enter the port number you found in your VPN app.
- Click OK when you're done.
- To verify it's working, after a few minutes you should see the small orange flame icon at the bottom of the qBittorrent window change into either a green plug or a green globe icon.

### Set up Split Tunneling (optional but recommended)
- In your VPN application, enable the option for split tunneling (Proton guide shown [**HERE**](https://protonvpn.com/support/protonvpn-split-tunneling#windows))
- In the Split Tunneling options, set qBittorrent to be "Included" in the VPN tunnel.
- Set all other applications to be "Excluded"

---

## Android

<div style="background: rgba(59, 130, 246, 0.1); border-left: 4px solid #3b82f6; padding: 1.5rem; margin: 2rem 0; border-radius: 0.5rem;">

**Android Limitations**

There are a number of downsides to torrenting on an Android device rather than a PC:
- Port forwarding generally not supported by VPN providers on Android.
- Inability to block file extensions.
- Many private trackers do not allow Android clients.

Still, torrenting CAN be done safely with the following recommendations.

</div>

### Installation
- Choose your VPN provider and install their application and sign in (download link for [**Proton**](https://play.google.com/store/apps/details?id=ch.protonvpn.android)).
- Choose a VPN server to connect to in the VPN application.
	- Pick the closest server with the best ping. It is not necessary to choose a server in another country.
	- If your provider has P2P specific servers (like Proton), then be sure to choose one of those.
- Install your torrent client ([**Flud**](https://play.google.com/store/apps/details?id=com.delphicoder.flud) highly recommended and will be used throughout this guide).

### Bind Your VPN to Your Torrent Client (critical)
- In Flud, go to Settings > Privacy and Security
	- Check the "VPN Only" box.
- Now in Flud, go to Settings > Advanced
	- Change the Network Interface from "Any" to the option that matches your VPN.
	- If you cannot determine which option is correct, try toggling your VPN off and on to see which option disappears / reappears from the list.

### Test Your VPN Binding (optional but recommended)
- Pause or remove all torrents currently in your torrent client
- Turn on your VPN
- Disable any kill switch you may use, we don't want to test the kill switch, we want to test the binding
- Go to ipleak.net
- Click "activate" button under "torrent address detection"
- Click "add this magnet link"
- Torrent will be added to your torrent client
- You should see only your VPN IP address in the browser in the "torrent adress detection" section (ignore all the other sections, they don't matter for torrenting)
- NOW, SHUT OFF YOUR VPN (leave your torrent client running)
- You should still see only your VPN IP in the torrent detection list (or nothing at all)
- IF AT ANY POINT YOU SEE YOUR HOME IP ADDRESS (in the "torrent adress detection" section), SOMETHING IS WRONG. Go back and retry VPN binding steps / choose different network adapter.
- Additional testing (optional): go to [**FossTorrents**](https://fosstorrents.com/distributions/arcolinux/), click the magnet link for ArcoNet (popular Linux Distro), let the torrent start and then verify that your download speed in your torrent client drops to zero when you disconnect from your VPN (will take a few minutes to drop all the way to zero).

### Set up Split Tunneling (optional but recommended)
- In your VPN application, enable the option for split tunneling (Proton guide shown [**HERE**](https://protonvpn.com/support/protonvpn-split-tunneling#android))
- In the Split Tunneling options, set Flud to be "Included" in the VPN tunnel.
- Set all other applications to be "Excluded"

---

## Torrent Sites

<div style="background: rgba(59, 130, 246, 0.1); border-left: 4px solid #3b82f6; padding: 1.5rem; margin: 2rem 0; border-radius: 0.5rem;">

**Prerequisites**

- Be sure to follow the guide above to safely set up your torrent client + VPN before proceeding, ESPECIALLY binding your VPN to your torrent client.
- Use [**Firefox**](https://www.firefox.com/) + [**uBlock Origin**](https://addons.mozilla.org/firefox/addon/ublock-origin/).
	- Firefox is the top non-Chromium browser. Google has been making changes to neuter ad blocking capability on its Chrome browser, and these changes are expected to eventually take effect Chromium-based browsers as well. 
	- Firefox also has the [**best compatibility**](https://github.com/gorhill/uBlock/wiki/uBlock-Origin-works-best-on-Firefox) with uBlock Origin, an addon that is very efficient at blocking ads and redirects. UBO is currently the most effective ad blocker. Do not assume that other ad blockers are sufficient, often times they are not.
	- Pirate sites are notorious for having malicious ads and redirects. Proper ad blocking is not simply a convenience, it is a NECESSITY for SAFETY.

</div>

- Choose a torrent site from [**FMHY's Torrent Sites List**](https://fmhy.net/torrenting).
- Heed warnings on FMHY specifically around software and games. These should only be sourced from a very specific subset of torrent options.

---

<div style="background: rgba(59, 130, 246, 0.1); border-left: 4px solid #3b82f6; padding: 1.5rem; margin: 2rem 0; border-radius: 0.5rem;">

**Guide Verification**

This guide was made by: [**LZ129Hindenburg**](https://www.reddit.com/user/LZ129Hindenburg/)

</div>