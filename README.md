[![Discord](https://badgen.net/discord/members/AxSSjpgwjx)](https://discord.gg/AxSSjpgwjx) 
## Home network internet bonding with Speedify
A router OS to easily setup Speedify as the main gateway using OpenWRT without command line usage. <br>Not affiliated with Speedify or Connectify.<br>
<br>
Typical use case examples: 
- Use Speedify as SDN bonding VPN to cover all connected devices in a home network when it's not practical to share a WAN per device.  
- Access to a reliable internet with usable speeds in a rural area or a corrupted country by bonding 2 or more connections, preferably a combination of wired and wireless with baseline ISP plans.
  
<img src="https://raw.githubusercontent.com/TalalMash/SmoothWAN-web/main/smoothwan-illust.drawio.svg" width="400"/> <br>
  
 ***
  
<details>
<summary>Basic Setup for the Raspberry Pi 4 using a smartphone</summary>
  
- Download and follow the instructions from Releases page to setup the microSD card. <br>
- Connect as the following diagram: <br>
<img src="https://github.com/TalalMash/SmoothWAN-web/raw/main/Basic%20Setup%20Guide%20assets/1a.svg" width="400"/> <br>
- The Raspberry Pi 4 (RPi4) is now broadcasting as a WiFi access point for easy configuration, connect to "SmoothWAN Setup", password: "brassworld": <br>
<img src="https://github.com/TalalMash/SmoothWAN-web/raw/main/Basic%20Setup%20Guide%20assets/1.png" width="300"/> <br>
- Visit: http://172.17.17.2 or for old versions: http://192.168.3.1 in your browser and login, there is no password set: <br>
<img src="https://github.com/TalalMash/SmoothWAN-web/raw/main/Basic%20Setup%20Guide%20assets/2.png" width="300"/> <br>
<img src="https://github.com/TalalMash/SmoothWAN-web/raw/main/Basic%20Setup%20Guide%20assets/3.png" width="300"/> <br>
- You will be greeted with brief instructions in the UI, setup Speedify: <br>
<img src="https://github.com/TalalMash/SmoothWAN-web/raw/main/Basic%20Setup%20Guide%20assets/4.png" width="300"/> <br>
- Click "Trigger Install/Update": <br>
<img src="https://github.com/TalalMash/SmoothWAN-web/raw/main/Basic%20Setup%20Guide%20assets/5.png" width="300"/> <br>
- Click "View Log" tab, it will show "Speedify is installed" at the end of the log after few seconds: <br>
<img src="https://github.com/TalalMash/SmoothWAN-web/raw/main/Basic%20Setup%20Guide%20assets/6.png" width="300"/> <br>
- Head to Status->Overview: <br>
<img src="https://github.com/TalalMash/SmoothWAN-web/raw/main/Basic%20Setup%20Guide%20assets/7.png" width="300"/> <br>
- You will be greeted with Speedify app, login: <br>
<img src="https://github.com/TalalMash/SmoothWAN-web/raw/main/Basic%20Setup%20Guide%20assets/8.png" width="300"/> <br>
- Time to connect and configure a Wi-Fi AP/router if needed, the internal Wi-Fi of the RPi4 is poor for general usage, connect using RPi4's Ethernet to a configured AP/router [(more info)](https://github.com/TalalMash/SmoothWAN/discussions/18#discussioncomment-2521688): <br>
<img src="https://github.com/TalalMash/SmoothWAN-web/raw/main/Basic%20Setup%20Guide%20assets/2a.svg" width="300"/> <br>
- After switching over to Wi-Fi AP/router, head over to Network->Wireless (Basic) and disable internal Wi-Fi: <br>
<img src="https://github.com/TalalMash/SmoothWAN-web/raw/main/Basic%20Setup%20Guide%20assets/12.png" width="300"/> <br>
<img src="https://github.com/TalalMash/SmoothWAN-web/raw/main/Basic%20Setup%20Guide%20assets/13.png" width="300"/> <br>
- Setup a password for SmoothWAN admin page in System->Administration <br>
- All done, enjoy a reliable internet! <br>

***

- <b>Extra</b>: to change the USB ports / WAN name, head to Interfaces->Multi-WAN USB: <br> 
<img src="https://github.com/TalalMash/SmoothWAN-web/raw/main/Basic%20Setup%20Guide%20assets/14.png" width="300"/> <br>
<img src="https://github.com/TalalMash/SmoothWAN-web/raw/main/Basic%20Setup%20Guide%20assets/15.png" width="300"/> <br>
<img src="https://github.com/TalalMash/SmoothWAN-web/raw/main/Basic%20Setup%20Guide%20assets/16.png" width="300"/> <br>
<img src="https://github.com/TalalMash/SmoothWAN-web/raw/main/Basic%20Setup%20Guide%20assets/17.png" width="300"/> <br>

</details>

<details> 
<summary>Speedify compared to current consumer-grade bonding solutions</summary>

- Suitable for non-streaming services with low buffer.  
- SDN VPN: By having one exit IP address, connected network sessions are uninterrupted. Flow control: sensitive streams packets are duplicated across WANs and prioritized for VoIP, video calls, streaming, and games for seamless failover and lossless connectivity even when combining lossy WANs. While non-sensitive streams packets are aggregated across WANs for the speed of the total combined WANs, and bulk downloads using single sockets are aggregated. Sensitive streams are also aggregated with high quality sources. <br>
- Per WAN quality rating system that's based on jitter, latency, stability, and speed variations over a period of time to prevent an unstable WAN from impacting total aggregation performance. e.g WAN resume and suspend delay is increased on multiple failures, poor connections will be removed from aggregation and used for backup etc. <br>
- Per WAN VPN transport protocols for optimal connectivity when used with strict ISPs or poor middleboxes, used protocols: HTTPS(disguises as web browsing), UDP, TCP, TCP Multiple. <br>
- "TCP Multiple" transport protocol as known as parallel transfer sockets similiar to threaded download managers. It allows maximum speed to be achieved on high latency, lossy, and far region VPN servers (with loss based CCA host settings and out-of-order packets). Also circumvents poor ISP restrictions. <br>
- Automatic packet aggregation weighing for largely asymmetric and heterogenous WANs. Slowly adapts to speed variations when using cellular/wireless. <br>
- No out of order packet delivery on aggregation with a reordering buffer, needed for single flow TCP connection performance. <br>
- An option for using a WAN for speed boosts only and backup only mode, data consumption usage depends on primary WAN quality rating in backup mode for seamless failover. <br>
- Switching critical settings such as protocols, modes, and adding or removing WANs without disruption. <br>
- TCP transport modes implements pacing for low RTT and low TCP-over-TCP overhead. <br>
- Instant server region selection for region restricted services. <br>
- Relatively affordable and does not require setting up a server. <br>
  
</details>

<details>
<summary>Advanced: Build from source using OpenWRT's imagebuilder</summary>
See Wiki for details: [Development Notes](https://github.com/TalalMash/SmoothWAN/wiki/Development-Notes)
</details>
  
 ***
  
Platforms: Raspberry Pi 4(~250Mbit chacha20), NanoPi R4S(~400Mbit+ AES) and 64-bit PC
<br>
Additional features: 
-  USB port agnostic for portable setups using persistent WAN configuration by MAC-addr for USB Ethernet adapters, 4G USB dongles* (RNDIS)  
-  Preset configuration for USB Ethernet adapters and tethering devices for plug and play (Raspberry Pi 4/NanoPi R4S) with interface renaming.  
-  Bypass Speedify with selective WAN for local devices/ports/domains using modified-[VPNBypass](https://docs.openwrt.melmac.net/vpnbypass/)  
-  [Pi-hole installer](https://github.com/TalalMash/SmoothWAN/wiki/Setting-up-Pi-hole) for local home network adblocking  
-  [Tailscale installer](https://github.com/TalalMash/SmoothWAN/wiki/Setting-up-Tailscale) for easy remote access to connected devices in your home network  
-  [Plug and play OLED display support](https://github.com/TalalMash/SmoothWAN/wiki/Setting-up-OLED-display-for-stats-(RPi4)) for displaying Speedify info  
-  Basic wireless setup menu for easy configuration with optimized presets (WIP)  
  
<sub>*NCM & QMI USB modems require manual configration instructed by ISP, setup in "Interfaces" page.</sub>


Use the discussions tab in Github for a forum-like discussion on networking configurations and Speedify topics, and issues tab for SmoothWAN related issues.  
Interactive discussion hub is hosted at Discord linked top. <br>
Libraries/Apps used are mentioned in Wiki. Credits are mentioned per release. <br>

[Buy me maté 🧉](https://www.paypal.com/paypalme/talalmsb/1)


