## Custom OpenWRT build for Speedify

An easy to use OpenWRT based flavor for Speedify with no CLI requirment.  
Typical use case: Deploy Speedify to your home network in minutes with few clicks.  

Targets: Raspberry Pi 4 and Generic x86_64 (+VM)  
Most modules were enabled, check config.*.info in buildconfigs. 

Use the discussions tab in Github for a forum-like discussion on networking configurations, and issues tab for SmoothWAN specifics.  
Interactive discussion server: https://discord.gg/AxSSjpgwjx  

<details> 
<summary>MACVLAN Example</summary>
<img src="https://raw.githubusercontent.com/TalalMash/SmoothWAN-web/main/macvlan.svg">
</details> <br>

Screenshots:
![image](https://user-images.githubusercontent.com/96490382/147124839-fdbf295e-932a-4a6f-87a7-a322605579c9.png)
![image](https://user-images.githubusercontent.com/96490382/147124822-ce79e50c-09a5-43ac-8f35-3ddb8b2be882.png)

<details> 
<summary>Why Speedify?</summary>
- SDWAN-esque: Having one exit IP address like any VPN, sessions are uninterrupted and it duplicates (mirror) data across WANs for sensitive connections such as VoIP, video calls, and games for "seamless migration" on fault for the speed of the fastest WAN while simulatenously aggregating (splitting) bulk data across WANs per packet for the speed of the combined WANs. (bulk data transfers tolerates hiccups). <br>
- Per-WAN rating system that's based on jitter, latency, stability, and speed variations over a period of time to prevent an unstable WAN from impacting total aggregation performance. (e.g increases faulty WAN action intervals between repetitive failures)<br>
- Per-WAN VPN transport protocol for best performance in Auto mode; Protocols: HTTPS(web browsing disguise), UDP, TCP, TCP Multi.<br>
- "TCP Multiple" transport protocol feature, A.K.A parallel transfer channels in other software, allows maximum speed to be achieved on high latency, lossy, and far VPN region servers with commonly used TCP congestion controllers. <br>
- Automatic packet aggregation weighing for largely asymmetric and heterogenous WANs. Slowly adapts to speed variations.<br>
- A buffer to reduce TCP reordering. <br>
- An option for using a WAN for boost only mode with configurable speed trigger and backup only mode (low data consumption, depends on primary WAN quality rating). <br>
- TCP transport mode implements pacing (effects: low UDP-over-TCP latency overhead, low bufferbloat.) <br>
- Instant server region selection for region restricted services. Other services require fixed IP/server. <br>
- Switching critical settings such as protocols, modes, and adding new WANs without measurable disruption other than latency variation on the aggregation channel. <br>
<br>
  Most of the observations listed were observed with Speedify's log files (comprehensive) and network simulation tools.
</details> <br>

[Buy me a ☕](https://www.paypal.com/paypalme/talalmsb/1)
