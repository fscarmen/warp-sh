# 【WGCF】Connect CF WARP to add IPv4/IPv6 network for servers

English | [中文](README.md)

* * *

# Table of Contents

- [Update Information](README_EN.md#update-information)
- [Script Features](README_EN.md#script-features)
- [WARP Benefits](README_EN.md#warp-benefits)
- [WARP Script Usage](README_EN.md#warp-script-usage)
- [WARP-GO Script Usage](README_EN.md#warp-go-script-usage)
- [Cloudflare API](README_EN.md#cloudflare-api)
- [How to brush Netflix Unlock WARP IP](README_EN.md#how-to-brush-netflix-unlock-warp-ip)
- [WARP socks5 or interface splitting template and unlock chatGPT method](README_EN.md#warp-socks5-or-interface-splitting-template-and-unlock-chatgpt-method)
- [WARP+ License and ID Acquisition](README_EN.md#warp-license-and-id-acquisition)
- [How to Obtain and Use WARP Teams for Linux](README_EN.md#how-to-obtain-and-use-warp-teams-for-linux)
- [WARP Principle](README_EN.md#warp-principle)
- [Acknowledgements to WARP Contributors and CloudFlare WARP Global Site Service Status List](README_EN.md#acknowledgements-to-warp-contributors-and-cloudflare-warp-global-site-service-status-list)

* * *

## Update Information
2026.03.01 warp-go.sh v1.3.2 Use fixed IP endpoints on IPv4-only / IPv6-only hosts.

2026.02.25 menu.sh v3.2.2 Restore Reserved configuration for Warp usage;

2026.02.22 mehu.sh v3.2.1 / warp-go.sh v1.3.1 1. Remove OS version checks to support rolling releases; 2. cloudflare.now.cc -> cloudflare.nyc.mn

2026.01.02 mehu.sh v3.2.0 / warp-go.sh v1.3.0 1. Account: Remove deprecated WARP+ and Teams account types from installation and upgrade processes (warp a) following Cloudflare's adjustments; 2. Bug Fix: Resolve networking breakdown by correcting routing rule handling during Linux Client removal in proxy mode; 3. Performance: Implement self-hosted IP API to significantly improve IP information retrieval speed; 4. Cleanup: Remove obsolete script prompts and redundant UI messages; 5. IP-Brushing Logic: Adjust default Netflix unlock preference from IPv4 to IPv6

<details>
    <summary>Historical Updates (click to expand or collapse)</summary>
<br>

>2025.09.10 menu.sh v3.1.8 Enhance the script's compatibility with Arch Linux and EndeavourOS systems.
>
>2025.08.24 menu.sh v3.1.7 1. Added support for installing Warp on Ubuntu 24.04 and later versions. Thanks to the solution provided by community member [Michaol]; 2. Added support for Client installation on Debian 13. Thanks to the feedback from user [ainp]
>
>2025.08.11 menu.sh v3.1.6 / warp-go.sh v1.2.4 Remove best endpoint feature to adapt to official adjustments;
>
>2025.03.24 menu.sh v3.1.5 1. Client's Warp mode (network interface) has been fixed to deal with the problem that it does not work after reboot; 2. Fixed the regularity of Team IPv6 judgment;
>
>2024.12.24 menu.sh v3.1.4 / warp-go.sh v1.2.3 Support Docker to externally listen on 0.0.0.0/0 without requiring the use of host network mode. Thanks to Bro @Anthony_Tel;
>
>2024.9.24 menu.sh v3.1.3 The Linux Client adds the MASQUE protocol option, available in both Proxy mode (menu 5) and WarpProxy mode (menu 14);
>
>2024.9.14 menu.sh v3.1.2 / warp-go.sh v1.2.2 1. Remove the function of generating licenses from the previous version because cloning Warp+ licenses is officially prohibited; 2. Remove unnecessary dependencies on python3;
>
>2024.7.25 menu.sh v3.1.1 / warp-go.sh v1.2.1 1. Support using the self-built WARP API at https://warp.cloudflare.now.cc/?run=pluskey to generate a 1920 PB WARP+ license for upgrading to a Plus account; 2. Client lacks sufficient support for WARP+, only able to use IPv4 and not IPv6; 3. Optimize the installer to further reduce script runtime;
>
>2024.7.18 menu.sh v3.1.0 / warp-go.sh v1.2.0 1. Use self-built warp api: https://warp.cloudflare.now.cc/ to upgrade to Teams account, no need to prepare Token in advance, only need to enter organization, email and verification code when the script is running to complete, the efficiency is greatly increased; 2. Because the Client's settings need to be set up in the Cloudflare dashboard, which can cause the vps to lose contact if not handled properly, the Client's is not upgraded to a Teams account, and the user can look up the information to set it up on their own;
>
>2024.7.8 menu.sh v3.0.10 / warp-go.sh v1.1.9 1. Publish warp api, you can register account, join Zero Trust, check account information and all other operations. Detailed instructions: https://warp.cloudflare.now.cc/ ; 2. Scripts to update the warp api;
>
>2024.6.30 menu.sh v3.0.9 1. By multithreading, parallel processing of optimal MTU, optimal endpoint, downloading wireguard-go and installing dependencies, the script runtime is reduced by more than half; 2. Reverse proxy http://ip-api.com/json and https://hits.seeyoufarm.com with cloudflare worker for better dual-stack support and faster fetching; 3. DNS Priority: Cloudflare 1.1.1.1 > Google 8.8.8.8;
>
>2024.6.28 menu.sh v3.0.8 The official WARP Linux Client supports arm64 systems and is available in both socks5 proxy and Warp interface modes;
>
>2024.6.2 menu.sh v3.0.7 Support CentOS 9 / Alma Linux 9 / Rocky Linux 9 system;
>
>2024.5.5 menu.sh v3.0.6 / warp-go.sh v1.1.8 Support Alpine edge system;
>
>2024.5.1 menu.sh v3.0.5 Deal with apt library changes for Debian 10 installations of wireguard-tools;
>
>2024.4.14 menu.sh v3.0.4 1. Alpine check and update the wget version; 2. Add a message for feedback when connect warp fails;
>
>2024.3.21 menu.sh v3.0.3 / warp-go.sh 1.1.7 1. Update some commands according to warp-cli; 2. Remove the github cdn;
>
>2024.2.7 menu.sh v3.0.2 To check if the WireGuard kernel module is already loaded. If not, attempt to load it and recheck;
>
>2023.12.19 menu.sh v3.0.1 / warp-go.sh 1.1.6 Add a check to see if udp is allowed, if all endpoints of WARP are unreachable, the script will abort;
>
>2023.8.22 menu.sh v3.0.0 / warp-go.sh 1.1.5 Add Github CDN;
>
>2023.8.15 menu.sh v3.0.0 1. Add a non-global working mode, it can be switched use [warp g], which requires a script reinstallation; 2. Support regions sanctioned by Cloudflare, such as Russia, with a shared account; 3. IPv6 only uses the preset nat64 and restores the original nameserver file when uninstalled;
>
>2023.7.21 menu.sh v3.0.0 beta2 1. If the system supports wireguard kernel and wireguard-go-reserved, it can be switched use [warp k], which requires a script reinstallation; 2. Support Fedora system; 3. Fix switch error caused by client version 2023.7.40-1;
>
>2023.6.30 menu.sh v3.0.0 beta IMPORTANT: 1. Use Cloudflare official warp api to replace wgcf; 2. Use wireguard-go with reserved to replace kernel. Make Hong Kong, Los Angeles and other restricted areas use warp; The above are the works of enthusiastic user, I would like to thank this guy and warp-go author coia for their contributions on behalf of all users of this script; 3. Since the changes are too big, please ask users to reinstall, if you have any problems, please feedback, I will deal with it as soon as possible;
>
>2023.6.27 menu.sh V2.53 Wireproxy proxy mode supports warp dualstack. From now on wgcf / wireproxy / client all support dual stack;
>
>2023.6.21 menu.sh V2.52 1. Client proxy mode supports warp dualstack; 2. Client warp mode supports warp dualstack; 3. Speed up script startup; Thanks to Bro ⑥, WordsWorthLess, us254 and chika0801 for the guidace on the xray template;
>
>2023.6.18 menu.sh V2.51 Client supports Debian 12 (bookworm);
>
>2023.5.20 menu.sh V2.50 1. Client supports IPv6 only VPS; 2. Support 4 ways to upgrade to teams account including token (Easily available at https://web--public--warp-team-api--coia-mfs4.code.run); 3. Use api to delete warp account while uninstalling;
>
>2023.5.15 Cloudflare API
>Thanks to badafans open source project and patient guidance. Now released in linux using the Cloudflare WARP API. [badafans open source project](https://github.com/badafans/warp-reg)
>Usage method
>```
>wget -N https://gitlab.com/fscarmen/warp/-/raw/main/api.sh && bash api.sh [option]
>```
>
>2023.5.10 warp-go V1.1.4 1. Docking the warp-go official account pool api, wiki: https://docs.zeroteam.top/apis/warp; 2. Change non-global from ipv4 only to dualstacks; 3. Fix the bug that the native IPv6 cannot login when using dualstacks; 4. Update the Best-enpoint app; 5. Change ip api;
>
>2023.3.26 warp-go V1.1.3 / menu.sh 2.49 1. Change the best Warp endpoint to standard ports [500,1701,2408,4500]; 2. Upgrade the Netflix unlocking section;
>
>2023.3.14 warp-go V1.1.2 / menu.sh 2.48 To speed up WARP, automatically find the most suitable endpoint for local use and apply it to wgcf, warp-go and client. Thanks to an anonymous and enthusiastic user for the tool;
>
>2023.3.2 warp-go V1.1.1 1. warp-go v1.0.8 is supported. Allowing custom MTU values in the configuration file /opt/warp-go/warp.conf; 2. Singbox configuration exports reseved using 3-numeric-array instead of a string;
>
>2023.2.22 [Unlock chatGPT without installing warp](README_EN.md#how-to-unlock-chatgpt-without-installing-warp)
>
>2023.2.7 menu.sh V2.47 Iptables + dnsmasq + ipset solution supports chatGPT. Install via the 12 option in the menu or `bash menu.sh e`;
>
>2022.12.17 warp-go V1.1.0 Support OpenWrt system;
>
>2022.12.10 warp-go V1.0.9 1.Export wireguard and sing-box config file with [warp-go e]; 2.Teams token website change to https://web--public--warp-team-api--coia-mfs4.code.run
>
>2022.10.19 menu V2.46 / warp-go V1.0.8 Switch the IPv4 / IPv6 priority by [warp s 4/6/d] or [warp-go s 4/6/d];
>
>2022.10.7 warp-go V1.0.7 1. Further improve the conversion function between accounts. You can even switch from one WARP+ to another; 2. Formatting code;
>
>2022.10.6 menu V2.45 1. Further improve the conversion function between accounts. You can even switch from one WARP+ to another; 2. Rebuild the account registration module;
>
>2022.9.10 Over 2,000 users star. Thank you to every solution creator. I'm just passing these on more widely to serve more players. Thank you to each user for your continued support. I wish you all good health and Happy Mid-Autumn Festival!
>
>2022.8.29 warp-go V1.0.6 1.Fixed the bug that routing rules failed after restart in non-global mode; 2.Fixed the bug of not changing IP;
>
>2022.8.27 menu V2.44 Refactoring the uninstallation logic. Dependency uninstallation requires confirmation;
>
>2022.8.23 menu V2.43 warp-go V1.0.5 Support NAT VPS. Such as Woiden;
>
>~2022.8.21 After testing, wgcf warp service is back to normal in Hong Kong and Toronto, etc.~
>
>2022.8.21 menu V2.42 1.Add shortcut hints in the menu; 2.Remove the shortcut of S. Single and dual stacks swithing can directly use [warp 4/6/d];
>
>2022.8.20 warp-go V1.0.4 Chinese and English language support. Hello World;
>
>2022.8.20 warp-go V1.0.3 New feat: Menu + shortcuts for various usage scenarios;
>
>2022.8.17 warp-go v1.0.2 1. Add WARP IPv4 non-global and global switch echo other. To use the v2ray/xray configuration file for triage, refer to the template for Client WARP mode on the project homepage; 2. Output wgcf configuration file (warp-go e);
>
>2022.8.13 warp-go v1.0.1 1.New feat: Support WARP+ (warp-go a <license>); 2.Support Teams (warp-go a token). You can easily get the token through https://warp-team-api.herokuapp.com/ ; 3.Brush unlock Netflix IP (warp-go i); 4.Support AMD v2 v3 v4  instruction set;
>
>2022.8.13 First on the whole web, proudly presents @CoiaPrant's warp-go one-click script. Using various interfaces of CloudFlare-WARP and integrating wireguard-go, it can completely replace WGCF. Save Hong Kong, Toronto, etc., and let VPS without official WARP also get WARP IP. Thanks @CoiaPrant and his team again. Project official address: https://gitlab.com/ProjectWARP/warp-go/-/tree/master/
>
>```
>wget -N https://gitlab.com/fscarmen/warp/-/raw/main/warp-go.sh && bash warp-go.sh [option] [lisence]
>```
>
>2022.8.5 2.41 1.Get the traffic quota of WARP+ via API. Thanks to Oreo for technical support;
>
>2022.6.27 Client installation method for Hong Kong IPv6 only, from LOC jhsyue's technical post: [wiki-hk-61.8 WARP tutorial](https://hostloc.com/thread-1036792-1-1.html)
>
>2022.6.11 2.40 1.Support VPS-free LXC VPS;
>
>2022.5.25 2.39  1.Automatically sync the latest official versions of wgcf, CloudFlare client, wireguard-go and wireproxy every day, allowing users to have the best performance with every installation; 2.Change the installation method of CloudFlare client, from APT/YUM repository to Package repository repository;
>
>2022.5.18 2.38 1. Fully support Ubuntu 22.04 and CentOS Streams 9 LTS; 2. Optimize Debian to speed up installation;
>
>2022.4.21 WARP one-click script on macOS. A VPN that fast,modern,secure by WireGuard tunnel and WARP service. The project address: https://github.com/fscarmen/warp/tree/main/pc
>
>2022.4.8  2.37 1. First publication on a global scale: After WirePorxy, another major technological breakthrough -- WARP-Cli's WARP mode solution. Thanks to the original creator -- Teacher LUBAN. It solves two major pain points: 1) The instability of the traditional proxy model; 2) Currently HK does not have a WARP service;
>
>2022.3.27  2.36 1. First publication on a global scale. By WireProxy, Wireguard client that exposes itself as a socks5 proxy; Thanks Fangliding for the information:[#113](https://github.com/fscarmen/warp/issues/113); 2. WARP+ and Teams can be used in WireProxy; 3. Systemd and change Netflix IP for WireProxy.
>
>2022.3.23  2.35 1.Support WARP on Debian9;
>
>Over 1,000 users star. Thank you for your support.
>
>2022.3.19  2.34: 1.Support Arch Linux. Thanks @SE_dong;
>
>2022.3.11  2.33: 1.First publication on a global scale. WARP Client support Ubuntu 18.04 and CentOS 7; 2. Open TUN for OVZ. You needn't setting it in the control panel. Thanks @Q_lilll;
>
>2022.2.25  2.32: 1.Change the WARP endpoint; 2. Sync the Netflix title with lmc999;
>
>2022.2.15 Happy Lantern Festival. Bring you a new experience of docker unlock, another way to unlock Netflix. Project based on alpine, content wgcf and unblocking Netflix scripts. Change unlock warp ip automatically. Project: https://github.com/fscarmen/unlock_warp
>
>2022.2.11  2.31: 1.iptables + dnsmasq + ipset to unlock stream media. (Not available for IPv6 only VPS). It is better than setting the outbound in xray/v2ray.
>
>2022.1.25  Media unlock daemon.  Check it every 5 minutes. If unlocked, the scheduled task exits immediately. If it is not unlocked, it will be swiped successfully in the background. Advantages: Minimized use of system resources. Please support professional unlock one-click script: https://github.com/fscarmen/unlock_warp
>
>```
>bash <(curl -sSL https://raw.githubusercontent.com/fscarmen/unlock_warp/main/unlock.sh)
>```
>
>2022.1.21  2.30: 1.All support WARP single-stack and dual-stack solutions. Switch to each other easily and quickly. Such as [warp s 4],[warp s 6],[warp s d]; 2.Brush Netflix Unlock IP with the expect area. Such as [warp i hk]. You can use it with crontab,screen,nohup & etc. [Detail](README_EN.md#how-to-brush-netflix-unlock-warp-ip); 3.Fixed stuck when brushing Netflix IP
>
>2022.1.11  2.26: 1.Asking the unlock Netflix region where you expect before brushing WARP IP; 2.Single and Dual stack switch to each other quickly.
>
>WARP docker solution support ARM64,AMD64 and s390x; 
>Dualstack on IPv4 only ,IPv6 only and native dualstack VPS is coming;
>
>2022.1.6  Major technical breakthrough. Successfully separate the WGCF configuration file from the environment dependencies. With the idea of everything can be Docker, using the ultra-lightweight Alpine as the base package (base package 5M + dependencies 22M = 27MB), the configuration is placed in the mapped directory to solve the problem that some old systems cannot use the WARP service.
>
>```
>wget -N https://cdn.jsdelivr.net/gh/fscarmen/warp/docker.sh && bash docker.sh [option] [lisence] ## Install docker, pull images and install containers
>
>docker exec -it wgcf sh #Some systems cannot run docker exec -it wgcf wg-quick up wgcf outside the container, you must execute it separately. Enter the container
>
>wg-quick up wgcf; exit #Run WGCF and exit the container.
>
>```
>
>![image](https://user-images.githubusercontent.com/62703343/148343358-67d0089a-591e-4af2-915c-e725422a5b0e.png)
>
>2022.1.1  1.Happy new year bros. I wish everyone good health and lots of money. Thanks for your support to this project. This project belongs to bros, I just summarized your fragmented information; 2.Add timestamp and running time while brushing Netflix IP.
>
>2021.12 29  You can try the scripts of two other WARP authors:
>1. Yongge ```wget -N https://cdn.jsdelivr.net/gh/kkkyg/CFwarp/CFwarp.sh && bash CFwarp.sh```
>2.P3terx ```bash <(curl -fsSL git.io/warp.sh) menu```
>
>2021.12.28  2.25: IMPORTANT: 1.First publication on a global scale. Support architecture s390x for IBM Linux One(Choose WARP ipv6 single stack),thx Brother Big B and Misaka; 2.Support Alpine Linux, thx Dong gua; 3.add whitelist. support Debian bookworm;
>
>2021.12.24  2.24: 1.The default language will set to the one selected during installation. ```echo 'E' >/etc/wireguard/language; warp v```; 2.Support HAX LXC VPS. It needs run ```until curl -s4m8 ip.gs; do warp n; done``` to brush the warp network;
>
>2021.12.17  2.23: Support change the Netflix IP not only WGCF but also Socks5 Client. Both will keep the Plus status. Recommand runs under [screen]; 2.Support update to TEAM account online. [URL for you](https://gist.githubusercontent.com/fscarmen/56aaf02d743551737c9973b8be7a3496/raw/16cf34edf5fb28be00f53bb1c510e95a35491032/com.cloudflare.onedotonedotonedotone_preferences.xml)
>
>2021.12.14  2.22: 1.First in the whole network. Use WARP Team account instead of Plus. No need to brush Plus traffic any more. 50 user limited. return to version 2.21;
>
>2021.12.11  2.21: 1.BoringTUN removed because of unstable; 2.Change the DNS to Google first. 3.Count the number of runs
>
>2021.12.04  2.20: IMPORTANT: First publication on a global scale. Reduce installation time by more than 50% through multi-threading. No need to wait for WGCF registering and MTU value searching time; 2.Recode EN/CH traslation through associative array. Smarter and more efficient. Thx Oreo.
>
>2021.11.30  2.11: Thanks to luoxue-bot for the original work and to huanxing dashen for the information. 1.Changing Netflix IP is adapted from other authors [luoxue-bot];
>
>2021.11.11  2.10: 1.Customize the priority of IPv4 / IPv6; 2.Customize the port of Client Socks5(default is 40000);
>
>2021.11.06  2.09: 1.WARP Linux Client supported.Socks5 proxy listening on: 127.0.0.1:40000. Register and connnect need non-WARP IPv4 interface. Native IPv4 + WARP IPv6 is ok; 2.WARP+ license on Client supported; 3.Customize the WARP+ device name.
>
>2021.11.01  2.08: 1.Serching the best MTU value for WARP interface automatically; 2.asn organisation for the VPS;
>
>2021.10.29  2.07: 1.Support Chinese and English; 2.Optimize running speed; 3.fix startup at reboot bug;
>
>2021.10.23  2.06: 1.Add automatic check if Tun module is enabled; 2.Improve script compatibility; 3.Add support for hax, Amazon Linux 2 and Oracle Linux
>
>2021.10.15  2.05: 1.WGCF automatically syncs to the latest 2.2.9; 2.Upgraded the method of running Warp after reboot, no longer dependent on another file; 3.Fix the bug of upgrading from free account to Warp+ account on KVM
>
>2021.10.14  2.04: 1.LXC users can choose BoringTun or Wireguard-go (BoringTun uses Rust language, performance close to kernel module performance, stability depends on VPS; WireGuard-GO uses Go language, performance is slightly worse than the former, high stability); 2.Add restriction: native dual-stack VPS can only use Warp dual-stack, bash menu.sh 1 will suggest changing to Warp dual-stack or exit; 3.After Warp network disconnection, running warp will automatically close the channel and kill the process; 4.After the script is aborted, use echo $? to display 1, which means unsuccessful (originally 0 representing successful operation)
>
>2021.10.12  2.03: 1.Optimized network brushing, accelerated the interval between two attempts, no dead loops will occur because the number of attempts has been limited to 10 times with clear prompts 2.Use Rust language BoringTun instead of Go language WireGuard-GO
>
>2021.10.10  2.02: The upstream ip.gs uses wget which is unstable and cannot get IP, causing continuous brushing. Abandoned and replaced with curl. The script automatically installs if not found
</details>

## Script Features

* Support WARP+ account, with third-party scripts to刷 WARP+ traffic and upgrade kernel BBR
* User-friendly menu for ordinary users, advanced users can quickly build through suffix options
* Intelligent judgment of VPS operating system: Ubuntu 16.04, 18.04, 20.04; Debian 9, 10, 11, CentOS 7, 8; Alpine and Arch Linux, please be sure to choose LTS system
  Intelligent judgment of hardware structure type: AMD, ARM and s390x
* Combining Linux version and virtualization method, automatically optimize three WireGuard solutions.
  Network performance: Kernel integrated WireGuard > Install kernel module > BoringTun > wireguard-go
* Intelligent judgment of the latest version of WGCF author's github repository (Latest release)
* Intelligent analysis of intranet and public IP to generate WGCF configuration file
* Output results, prompt whether to use WARP IP, IP location

## WARP Benefits

* Support chatGPT, unlock Netflix streaming media
* Avoid Google verification code or use Google Scholar
* Can call IPv4 interface, so that projects such as Qinglong and V2P can run normally
* Since data can be transmitted in both directions, it can be used as a jump board and probe of the other party's VPS, replacing HE tunnelbroker
* Can make nodes built on IPv6 only VPS support Telegram
* Nodes built with IPv6 can be used on PassWall and ShadowSocksR Plus+ that only support IPv4

<img src="https://user-images.githubusercontent.com/62703343/144635014-4c027645-0e09-4b84-8b78-88b41f950627.png" width="80%" />

## WARP Script Usage

First run
```
wget -N https://gitlab.com/fscarmen/warp/-/raw/main/menu.sh && bash menu.sh [option] [lisence/url/token]
```
Run again
```
warp [option] [lisence]
```
  | [option] Variable1 Variable2 | Specific action description |
  | ----------------- | --------------- |
  | h | Help |
  | 4 | Original status -> WARP IPv4 |
  | 4 lisence name | Add WARP+ Lisence and device name, such as ```bash menu.sh 4 N5670ljg-sS9jD334-6o6g4M9F Goodluck``` |
  | 6 | Original status -> WARP IPv6 |
  | d | Original status -> WARP dual stack |
  | o | WARP switch, the script actively judges the current status, automatically turns on or off |
  | u | Uninstall WARP |
  | n | For brushing WARP network when disconnected (WARP bug) |
  | b | Upgrade kernel, enable BBR and DD |
  | p | Brush Warp+ traffic |
  | c | Install WARP Linux Client, enable Socks5 proxy mode |
  | l | Install WARP Linux Client, enable WARP mode |
  | c lisence | Add WARP+ Lisence on the basis of the above, such as ```bash menu.sh c N5670ljg-sS9jD334-6o6g4M9F``` |
  | r | WARP Linux Client switch |
  | v | Sync script to the latest version |
  | i | Change WARP IP |
  | e | Install iptables + dnsmasq + ipset streaming media splitting solution |
  | w | Install WireProxy solution |
  | y | WireProxy switch |
  | k | Switch wireguard kernel / wireguard-go-reserved |
  | g | Switch warp global / non-global or install in non-global mode for the first time |
  | s | s 4/6/d, switch priority warp IPv4 / IPv6 / default  |
  | Others or empty value| Menu interface |

Example: To add Warp dual stack to Oracle IPv4 for the first time
```
wget -N https://gitlab.com/fscarmen/warp/-/raw/main/menu.sh && bash menu.sh d
```
Brush Japanese Netflix
```
warp i jp
```

## WARP-GO Script Usage
First run
```
wget -N https://gitlab.com/fscarmen/warp/-/raw/main/warp-go.sh && bash warp-go.sh [option] [lisence]
```
Run again
```bash
warp-go [option] [lisence]
```
  | [option] Variable1 Variable2 | Specific action description |
  | ----------------- | --------------- |
  | h | Help |
  | 4 | Original status -> WARP IPv4 |
  | 4 lisence name | Add WARP+ Lisence and device name, such as ```bash wire-go 4 N5670ljg-sS9jD334-6o6g4M9F Goodluck``` |
  | 6 | Original status -> WARP IPv6 |
  | d | Original status -> WARP dual stack |
  | o | warp-go switch, the script actively judges the current status, automatically turns on or off |
  | u | Uninstall warp-go |
  | v | Sync script to the latest version |
  | Others or empty value| Menu interface |

## Cloudflare API

### Cli-API User Guide, browser access with parameters, or use `curl` command to execute Warp API requests,

| run parameter | Description | Parameters | Example |
|---|---|---|---|
|  | User Guide | | `https://warp.cloudflare.now.cc/` |
| `register` | Register new device | `team_token (optional)`, `format (optional)` | `https://warp.cloudflare.now.cc/?run=register&team_token=<Your-Team-Token>&format=<json\|yaml\|client\|wireguard\|warp-go\|\|clash\|xray\|sing-box\|qrencode>` |
| `device` | Get detailed information of a specific device | `device_id`, `token` | `https://warp.cloudflare.now.cc/?run=device&device_id=<Your-Device-ID>&token=<Your-Token>` |
| `app` | Get client configuration | `token` | `https://warp.cloudflare.now.cc/?run=app&token=<Your-Token>` |
| `bind` | Bind device to account | `device_id`, `token` | `https://warp.cloudflare.now.cc/?run=bind&device_id=<Your-Device-ID>&token=<Your-Token>` |
| `name` | Set device name | `device_id`, `token`, `device_name` | `https://warp.cloudflare.now.cc/?run=name&device_id=<Your-Device-ID>&token=<Your-Token>&device_name=<Your-Device-Name>` |
| `license` | Set device license | `device_id`, `token`, `license` | `https://warp.cloudflare.now.cc/?run=license&device_id=<Your-Device-ID>&token=<Your-Token>&license=<Your-License>` |
| `unbind` | Unbind device from account | `device_id`, `token` | `https://warp.cloudflare.now.cc/?run=unbind&device_id=<Your-Device-ID>&token=<Your-Token>` |
| `cancel` | Cancel device registration | `device_id`, `token` | `https://warp.cloudflare.now.cc/?run=cancel&device_id=<Your-Device-ID>&token=<Your-Token>` |
| `id` | Client ID and Reserved conversion | `convert` | `https://warp.cloudflare.now.cc/?run=id&convert=<4-char-string\|Numbers1,Numbers2,Numbers3>` |
| `token` | Get Zero Trust token | `organization`, `email`, `code` | step1: `https://warp.cloudflare.now.cc/?organization=<Your-Organization>&email=<Your-Email>` </br> step2: `https://warp.cloudflare.now.cc/?organization=<Your-Organization>&cf_appsession=<App-Session-Value>&cf_session=<Session-Value>&nonce=<Nonce-Value>&code=<Your-Code>` |
| `key` | Generate a pair of WireGuard public and private keys | `format (optional)` | `https://warp.cloudflare.now.cc/?run=key&format=<json\|yaml>` |

### Shell-API Script Usage
```
wget -N https://gitlab.com/fscarmen/warp/-/raw/main/api.sh && bash api.sh [option]
```
  | [option] Variable  | Specific action description |
  | ------------- | ------------- |
  | -h/--help     | Help |
  | -f/--file     | File to save account registration information, supporting official api, client, wgcf and warp-go. If not filled, manually enter device id and api token |
  | -r/--register | Register account |
  | -t/--token    | When registering with -r, use team token to register, quick access: https://web--public--warp-team-api--coia-mfs4.code.run |
  | -d/--device   | Get account registration information, including plus traffic, etc. |
  | -a/--app      | Get app information |
  | -b/--bind     | Get bound device information, including sub-devices |
  | -n/--name     | Modify device name |
  | -l/--license  | Modify license |
  | -u/--unbind   | Unbind device |
  | -c/--cancle   | Cancel account |
  | -i/--id       | Display cliend id and reserved |

## How to Brush Netflix Unlock WARP IP

* You can use another one-click script that unlocks streaming media through WARP: [【Brush WARP IP】 - Born for WARP to unlock streaming media](https://github.com/fscarmen/unlock_warp)

* Taking brushing Hong Kong hk as an example, run `warp i`. It is recommended to run in the background with screen or nohup

* If the unlock IP has not been brushed out for a long time, you can check whether CloudFlare is maintaining the route locally: https://www.cloudflarestatus.com/

## WARP socks5 or interface splitting template and unlock chatGPT method

<details>
    <summary> Xray configuration template for assigning websites to socks5 (suitable for WARP Client Proxy and WireProxy) (click to expand or collapse)</summary>
<br>

Local socks5://127.0.0.1:40000
Taking [mack-a's eight-in-one script](https://github.com/mack-a/v2ray-agent) as an example. Edit ```/etc/v2ray-agent/xray/conf/10_ipv4_outbounds.json```

```
{
    "outbounds":[
        {
            "protocol":"freedom"
        },
        {
            "tag":"warp",
            "protocol":"socks",
            "settings":{
                "servers":[
                    {
                        "address":"127.0.0.1",
                        "port":40000 // Fill in your socks5 port
                    }
                ]
            }
        },
        {
            "tag":"WARP-socks5-v4",
            "protocol":"freedom",
            "settings":{
                "domainStrategy":"UseIPv4"
            },
            "proxySettings":{
                "tag":"warp"
            }
        },
        {
            "tag":"WARP-socks5-v6",
            "protocol":"freedom",
            "settings":{
                "domainStrategy":"UseIPv6"
            },
            "proxySettings":{
                "tag":"warp"
            }
        }
    ],
    "routing":{
        "rules":[
            {
                "type":"field",
                "domain":[
                    "geosite:openai",
                    "ip.gs"
                ],
                "outboundTag":"WARP-socks5-v4"
            },
            {
                "type":"field",
                "domain":[
                    "geosite:google",
                    "geosite:netflix",
                    "p3terx.com"
                ],
                "outboundTag":"WARP-socks5-v6"
            }
        ]
    }
}
```
</details>

<details>
    <summary> Xray configuration template for assigning websites to "interface" (suitable for WARP Client Warp and warp / warp-go non-global) (click to expand or collapse)</summary>
<br>

```
{
    "outbounds":[
        {
            "protocol":"freedom"
        },
        {
            "tag":"WARP-interface-v4",
            "protocol":"freedom",
            "settings":{
                "domainStrategy":"UseIPv4"
            },
            "streamSettings":{
                "sockopt":{
                    "interface":"CloudflareWARP", // For warp non-global mode, fill in warp; for Client's Proxy mode, fill in CloudflareWARP; for warp-go, fill in WARP
                    "tcpFastOpen":true
                }
            }
        },
        {
            "tag":"WARP-interface-v6",
            "protocol":"freedom",
            "settings":{
                "domainStrategy":"UseIPv6"
            },
            "streamSettings":{
                "sockopt":{
                    "interface":"CloudflareWARP",
                    "tcpFastOpen":true
                }
            }
        }
    ],
    "routing":{
        "domainStrategy":"AsIs",
        "rules":[
            {
                "type":"field",
                "domain":[
                    "geosite:google",
                    "geosite:openai",
                    "ip.gs"
                ],
                "outboundTag":"WARP-interface-v4"
            },
            {
                "type":"field",
                "domain":[
                    "geosite:netflix",
                    "p3terx.com"
                ],
                "outboundTag":"WARP-interface-v6"
            }
        ]
    }
}
```
</details>

<details>
    <summary> How to unlock chatGPT through WARP (click to expand or collapse)</summary>
<br>

The idea is to use the already registered warp to set up chained proxy. This solution is the most lightweight, and users only need xray. The specific method is to modify the outbound and routing of the xray configuration file. The template is as follows:
```
{
    "outbounds":[
        {
            "protocol":"freedom",
            "tag": "direct"
        },
        {
            "protocol":"wireguard",
            "settings":{
                "secretKey":"YFYOAdbw1bKTHlNNi+aEjBM3BO7unuFC5rOkMRAz9XY=", // Paste your "private_key" value
                "address":[
                    "172.16.0.2/32",
                    "2606:4700:110:8a36:df92:102a:9602:fa18/128"
                ],
                "peers":[
                    {
                        "publicKey":"bmXOC+F1FxEMF9dyiK2H5/1SUtzH0JuVo51h2wPfgyo=",
                        "allowedIPs":[
                            "0.0.0.0/0",
                            "::/0"
                        ],
                        "endpoint":"engage.cloudflareclient.com:2408" // Or fill in 162.159.192.1:2408 or [2606:4700:d0::a29f:c001]:2408
                    }
                ],
                "reserved":[78, 135, 76], // Paste your "reserved" value
                "mtu":1280
            },
            "tag":"wireguard"
        },
        {
            "protocol":"freedom",
            "settings":{
                "domainStrategy":"UseIPv4"
            },
            "proxySettings":{
                "tag":"wireguard"
            },
            "tag":"warp-IPv4"
        },
        {
            "protocol":"freedom",
            "settings":{
                "domainStrategy":"UseIPv6"
            },
            "proxySettings":{
                "tag":"wireguard"
            },
            "tag":"warp-IPv6"
        }
    ],
    "routing":{
        "domainStrategy":"AsIs",
        "rules":[
            {
                "type":"field",
                "domain":[
                    "geosite:openai",
                    "ip.gs"
                ],
                "outboundTag":"warp-IPv4"
            },
            {
                "type":"field",
                "domain":[
                    "geosite:netflix",
                    "p3terx.com"
                ],
                "outboundTag":"warp-IPv6"
            }
        ]
    }
}
```
</details>

## WARP+ License and ID Acquisition

The following is the official introduction to Argo 2.0 after using WARP and Team: [Argo 2.0: Smart Routing Learns New Tricks](https://blog.cloudflare.com/argo-v2/)

Quote from Luminous: Actual tests show that WARP+ has no difference from the free version in terms of speed when accessing non-CF websites. Only when accessing CloudFlare sites, the paid version will use Argo-like technology to go to the origin through a data center closer to the target, while the free version is limited to going to the origin from the connection location, that's all.

<img src="https://user-images.githubusercontent.com/62703343/136070323-47f2600a-13e4-4eb0-a64d-d7eb805c28e2.png" width="70%" />

## How to Obtain and Use WARP Teams for Linux

* https://warp-token.cloudflare.nyc.mn/ , through fscarmen's website

* https://web--public--warp-team-api--coia-mfs4.code.run/, through Coia's website

## WARP Principle

WARP is a network traffic security and acceleration service based on WireGuard provided by CloudFlare, which can enable you to achieve privacy protection and link optimization by connecting to CloudFlare's edge nodes.

Its connection entry is dual-stack (both IPv4/IPv6 are available), and after connection, you can obtain NAT-based IPv4 and IPv6 addresses provided by CF. Therefore, our single-stack server can try to connect to WARP to obtain additional network connectivity support. This way, we can let servers with only IPv6 access IPv4, and also let servers with only IPv4 obtain IPv6 access capabilities.

* Add IPv4 to IPv6-only servers

As shown in the figure, IPv4 traffic is taken over by the WARP network card, realizing that IPv4 traffic accesses the external network through WARP.

<img src="https://user-images.githubusercontent.com/62703343/135735404-1389d022-e5c5-4eb8-9655-f9f065e3c92e.png" width="70%" />

* Add IPv6 to IPv4-only servers

As shown in the figure, IPv6 traffic is taken over by the WARP network card, realizing that IPv6 traffic accesses the external network through WARP.

<img src="https://user-images.githubusercontent.com/62703343/135735414-01321b0b-887e-43d6-ad68-a74db20cfe84.png" width="70%" />

* Network replacement for dual-stack servers

Sometimes our server itself is dual-stack, but for various reasons we may not want to use one of the networks. In this case, we can also use WARP to take over part of the network connection to hide our IP address. The purpose of doing this, the biggest significance is to reduce the probability of verification codes appearing in some severely abused data centers; at the same time, some content providers treat WARP's landing IP as the native IP of real users, which can lift some IP-based blockades.

<img src="https://user-images.githubusercontent.com/62703343/135735419-50805ed6-20ea-4440-93b4-5bcc6f2aca9b.png" width="70%" />

* Network performance: Kernel integrated > Kernel module > wireguard-go

## Acknowledgements to WARP Contributors and CloudFlare WARP Global Site Service Status List

The Internet never forgets, but people do.

Technical articles or related projects (in no particular order):
* P3terx: https://p3terx.com/archives/use-cloudflare-warp-to-add-extra-ipv4-or-ipv6-network-support-to-vps-servers-for-free.html
* P3terx: https://github.com/P3TERX/warp.sh/blob/main/warp.sh
* Oreomeow: https://github.com/Oreomeow
* Luminous: https://luotianyi.vc/5252.html
* Hiram: https://hiram.wang/cloudflare-wrap-vps
* Cloudflare: https://pkg.cloudflareclient.com/   
https://blog.cloudflare.com/announcing-warp-for-linux-and-proxy-mode/   
https://blog.cloudflare.com/argo-v2/
* WireGuard: https://lists.zx2c4.com/pipermail/wireguard/2017-December/002201.html
* Parker C. Stephens: https://parkercs.tech/cloudflare-for-teams-wireguard-config/
* Anemone: https://cutenico.best/posts/blogs/cloudflare-warp-fixed-youtube-location/    
https://github.com/acacia233/Project-WARP-Unlock
* wangying202: https://blog.csdn.net/wangying202/article/details/113178159
* LUBAN: https://github.com/HXHGTS/Cloudflare_WARP_Connect
* valetzx: https://gitlab.com/valetzx/pubfile
* badafans cf api: https://github.com/badafans/warp-reg
* chika0801: https://github.com/chika0801/Xray-examples/
* xXcmd1152Xx: https://github.com/cmd1152/WarpPlusKeyGenerator-NG-lib
* All enthusiastic netizens

Service providers (in no particular order):
* fscarmen's Warp API: https://warp.cloudflare.now.cc/
* fscarmen's Zero Trust Token API: https://warp-token.cloudflare.nyc.mn/
* CloudFlare Warp(+): https://1.1.1.1/
* Original author of WGCF project: https://github.com/ViRb3/wgcf/
* Coia and warp-go team: https://gitlab.com/ProjectWARP/warp-go
* warp-go api wiki: https://docs.zeroteam.top/apis/warp
* WireGuard-GO official: https://git.zx2c4.com/wireguard-go/
* ylx2016's mature work: https://github.com/ylx2016/Linux-NetSpeed
* ALIILAPRO's mature work: https://github.com/ALIILAPRO/warp-plus-cloudflare
* mixool's mature work: https://github.com/azples/across/tree/main/wireguard
* luoxue-bot's mature work:https://github.com/luoxue-bot/warp_auto_change_ip
* lmc999's mature work: https://github.com/lmc999/RegionRestrictionCheck
* WireProxy author: https://github.com/pufferffish/wireproxy
* Public IP and location query: https://ifconfig.co/ , https://ip.gs/ , https://ip.sb/ , https://ip-api.com
* PV statistics website: https://hits.seeyoufarm.com/
* Coia's web version to extract Teams Token: https://web--public--warp-team-api--coia-mfs4.code.run

CloudFlare WARP Global Site and Service Status:
* Operational = Normal. Re-routed = Maintenance status: https://www.cloudflarestatus.com/