# 1. 0x360 Physical and Link

- [1. Physical Layer](#1-physical-layer)
    - [Physical Media](#physical-media)
        - [1.1.2. Copper](#112-copper)
            - [Dial-Up](#dial-up)
            - [DSL](#dsl)
        - [Cable](#cable)
        - [1.1.1. Fiber](#111-fiber)
        - [Terrestrial Radio Channels](#terrestrial-radio-channels)
        - [Satellite Radio Channels](#satellite-radio-channels)
    - [1.1. Ethernet (IEEE 802.3)](#11-ethernet-ieee-8023)
    - [1.2. Wireless LAN (IEEE 802.11)](#12-wireless-lan-ieee-80211)
- [2. Data Link Layer (2)](#2-data-link-layer-2)
    - [2.1. MAC](#21-mac)
    - [2.2. ARP (Address Resolution Protocol)](#22-arp-address-resolution-protocol)
        - [2.2.1. Protocol](#221-protocol)
        - [2.2.2. Command](#222-command)
        - [2.2.3. Security](#223-security)
    - [2.3. NDP (Neighbor Discovery Protocol)](#23-ndp-neighbor-discovery-protocol)
    - [2.4. Hardware](#24-hardware)
- [3. Reference](#3-reference)

## 1. Physical Layer

### Physical Media
#### 1.1.2. Copper

twisted pair, the UTP (Unshielded twisted pair) is still common for LAN cables.

10/100/1000/10GBASE-T

The ISP is usally the local wired telephone companies (telco).

##### Dial-Up
Traditionally, most of the Internet users connect Internet over ordinary analog telephone line using a dial-up modem. Phone call and Internet access cannot be done at the same time.

##### DSL
Usually ADSL (Asymmetric Digital Subscriber Line), with which download speed is much faster than the upload speed. For business, there is the SDSL (symmetric) version.

DSL uses different frequencies to encode phone call and network access. For example, one configuration can be as follows:
- phone: 0 ~ 4kHz
- upload: 4kHz - 50kHz
- download 50kHz - 1MHz

#### Cable
Coaxial Cable is quite common in cable television systems, so the ISP is uslaly the television company. The disadvantage is the cable is shared by neighborhood, therefore requires some protocols to coordinate transmissions and avoid collisions. (e.g: CSMA/CD)

#### 1.1.1. Fiber

1000BASE-X

Submarine cables

*   [faster cable](https://techcrunch.com/2016/06/29/google-backed-undersea-cable-between-us-and-japan-goes-online-tonight/): 60 Tbps bandwidth
*   [interesting visualization](https://www.youtube.com/watch?v=IlAJJI-qG2k)
*   [How to repair](https://www.youtube.com/watch?v=MDSgYGL7gHc) :)


#### Terrestrial Radio Channels
carry signals in the elctromagnetic spectrum, spanning from 10~100m (e.g: wifi) and ~10km (e.g: cellular access)

#### Satellite Radio Channels
Two types aof satellite are used
- geostationary satellites: stationary over the same spot on Earth (about 36,000 km), siginificant communication delay.
- low-earth orbiting satellites: much closer (2,000 km), rotate around Earch and might communicate with each other. (SpaceX's StarLink is this type)

Note GPS is around 20,000km, ISS is around 400 km

### 1.1. Ethernet (IEEE 802.3)



### 1.2. Wireless LAN (IEEE 802.11)

## 2. Data Link Layer (2)

### 2.1. MAC

*   unique **48** bit for each hardware
*   <g class="gr_ gr_64 gr-alert gr_gramm gr_inline_cards gr_run_anim Grammar only-ins doubleReplace replaceWithoutSep" id="64" data-gr-id="64">each m</g>ac address is associated with **NIC** (network interface card)
*   _OUI_ (Organizationally Unique Identifier) is the first three <g class="gr_ gr_4 gr-alert gr_spell gr_inline_cards gr_run_anim ContextualSpelling ins-del multiReplace" id="4" data-gr-id="4">octats</g>

### 2.2. ARP (Address Resolution Protocol)

ARP is <g class="gr_ gr_4 gr-alert gr_gramm gr_inline_cards gr_run_anim Grammar multiReplace" id="4" data-gr-id="4">a IPv4</g> Protocol defined at RFC0826, it is used to translate <g class="gr_ gr_5 gr-alert gr_gramm gr_inline_cards gr_run_anim Grammar only-ins doubleReplace replaceWithoutSep" id="5" data-gr-id="5">32bit</g> IP address into 48bit MAC address.RFC0826

![ARP](../../img/arp.png)

reference: from TCP/IP Illustrated, Volume 1: The protocols

#### 2.2.1. Protocol

*   **ARP cache:** store arp records in <g class="gr_ gr_245 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Grammar only-ins doubleReplace replaceWithoutSep" id="245" data-gr-id="245">cache</g>, TTL is typically 20 min.
*   **ARP request**: If not in cache or expired, broadcast an ethernet frame under the subnet mask to request a MAC address corresponding to an IP.
*   **ARP reply**: NIC with the MAC address reply to the request with unicast. Other NICs will ignore the requests (although they can see the broadcast request)

#### 2.2.2. Command

*   arp -a: retrieval local arp cache

#### 2.2.3. Security

*   **arp spoofing**: man in the middle attack (ettercap)
*   **mac flooding**


### 2.3. NDP (Neighbor Discovery Protocol)

*   IPv6 Protocol as a replacement of ARP

### 2.4. Hardware

L2 Switch


## 3. Reference

[1] TCP/IP Illustrated, Volume 1: The protocols Chapter 4
