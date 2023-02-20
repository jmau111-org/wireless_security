# Wireless Security

Practical guide to introduce wireless technologies and associated vulnerabilities 🧢

![GitHub last commit](https://img.shields.io/github/last-commit/jmau111-org/wireless_security?label=last%20update%3A)

## Common wireless technologies

"Wireless" is a very broad term that covers a large range of techniques, devices, and situations. However, people usually refer to **WiFi** and **Bluetooth**.

These wireless connections are pretty convenient to setup and use, but there are some important limits to know.

### Wi-Fi in very short

WiFi or "Wireless Fidelity" is a technology used to provide Internet access to multiples devices without physical cables. The router is connected to Internet through a wired connection, but the connected devices receive and transmit data through radio waves, which are electromagnetic signals with a specific frequency (e.g., 2.4 GHz vs. 5 GHz).

Many electronic devices have a built-in WiFi adapter to exchange data with the router using the right protocol ([IEEE](https://en.wikipedia.org/wiki/Institute_of_Electrical_and_Electronics_Engineers) standards). 

Although, the quality of the connection can be affected by the number of connected devices or the distance to the router. Besides, interferences happen frequently.

WiFi has built-in security mechanisms to avoid unauthorized access to data, but there are documented vulnerabilities and attacks.

### Tethering in very short

Roughly speaking, the idea is to tether a device to another device that is connected to internet, for example, a smartphone or a laptop. In other words, it can consist of sharing the Internet access through a WiFi network or pairing devices with Bluetooth.

You may read similar terms like "mobile hotspot" or "mobile internet sharing."

It's often used as an alternative solution when the ISP or the Internet box is down or too slow. It's also not uncommon during events and conferences, when there's no router available.

It's convenient but has some cons. For example, it may consume lots of data, so it's probably better to use it as a last resort to avoid extra charges.

### Bluetooth in very short

Like WiFi, Bluetooth allows exchanging data over short distances without cables using radio waves. This protocol is meant for data transfer and has security mechanisms to protect its users.

However, there are important differences in speed and power consumption. You will likely choose WiFi for internet connectivity, as it has a longer range and a better speed overall.

You might even find that WiFi has a stronger encryption and better authentication mechanisms.

People usually prefer Bluetooth to connect low-power devices, such as headphones, to their smartphones. Still, it might also be used to tether Internet access.

## Common attacks and vulnerabilities

It's essential to list common attacks, again and again, as there are POCs (proofs of concept), open-source utilities, and even step-by-step demos in video available publicly, which lowers the barrier to entry for attackers significantly.

While the techniques are constantly evolving, here are some scenarios.

### Wifi attacks

#### Man-in-the-middle (MitM) attacks 

The communication between two devices connected to the same WiFi network may be intercepted and modified to steal confidential data or inject malicious payloads.

#### Rogue access point

Fake WiFi access points can mimic the legitimate ones and trick users into giving their credentials and many other sensitive data.

#### Weak encryption 

WiFi security has been constantly improving over the past years, but older versions of the protocol are still available on some Internet Boxes, which can result in MitM attacks because of weak encryption.

Use the latest one. At the time of writing, WPA 2 or WPA 3 are fine, but not WPA or WEP.

#### Password cracking

If the WiFi network relies on a weak password, attackers could crack it to gain unauthorized access.

#### Denial-of-service (DoS)

It's possible to flood a device with connection requests or data packets to crash it or deny its access.

There are documented techniques such as **Deauth** (sending deauthenticating packets to prevent the device from reconnecting) or **jamming** (~ generating radio frequency interferences).

### Bluetooth attacks

Most of the time, adversaries will enumerate nearby Bluetooth devices that are **discoverable** to find weaknesses and attack.

#### Bluejacking

Bluetooth Hijacking consists of sending unsolicited messages to a device to annoy the victims or attack them with social engineering techniques.

Although, modern devices have built-in security to block such attempts.

#### Bluesnarfing

The attackers may find vulnerable devices and gain access to steal sensitive information like contact lists, SMS, emails, and other data.

#### Denial-of-service (DoS)

Pretty much like WiFi DoS attacks (the general idea), but against Bluetooth-enabled devices. A typical example is the "Bluetooth ping flood attack."

#### Bluebugging

Adversaries may take full control of a vulnerable device without the user's consent. They need to be quite close to the victims, but 10 meters is a relatively long distance that can correspond to various situations.

#### Eavesdropping

Attackers could intercept the communication between two vulnerable devices using a Bluetooth scanner or sniffer, allowing them to decode the Bluetooth signal and steal sensitive data.

There are related techniques like "car whispering" where adversaries target car radios and eavesdrop on conversations or phone calls made inside the car.

#### BlueBorne hacks

[These hacks](https://www.armis.com/research/blueborne/) spread over the air (airborne) and don't even require attackers to pair with the targeted device, and can work even if the device is not in discoverable mode!

## How to protect wireless connections

### Bad approaches to avoid (IMHO)

While some articles may beg to differ, the following techniques aren't valuable **in a security perspective**.

#### Hidden SSIDs

WiFi settings allows "hiding" your Service Set IDentifier (SSID), but this information will be sent unencrypted during the negotiation process anyway.

If you suspect someone is trying to hack your connection, he will likely use a sniffer or a traffic monitoring software to discover your SSID.

#### MAC Address Filtering

Each device has a MAC address. It's possible to configure the router to whitelist specific MAC addresses, which seems a good idea, at first sight, but there are two major issues:

1. Your MAC address is sent along with network packets to ensure everything is delivered correctly
2. Cybercriminals can spoof whitelisted MAC addresses (e.g., using SMAC)

In a nutshell, **it's not a security feature**.

### Wired vs. wireless: the useless debate

It's not uncommon to read that wired connections are more secure than wireless connections. Indeed, radio waves seem more prone to eavesdropping or MitM attacks.

Although, wired connections are not immune to attacks. **Nothing** is inherently secured.

Beyond that, security should prevail over convenience but not usability. A wired connection might be "harder" to intercept, but there are other ways.

### 7 effective mitigations

* keep devices up-to-date
* use long and random passwords to secure access
* use robust encryption: use the latest security protocols (WPA2-AES, WPA 3)
* be cautious when pairing devices with unfamiliar devices, and don't connect cheap wireless accessories that lack strong encryption or rely on out-of-date firmware
* use firewalls and monitor your network for unusual traffic patterns (in corporate environments, you can also leverage network segmentation and intrusion detection systems)
* don't let your devices discoverable when not in use
* deactivate **unnecessary** network services and protocols

### Underrated strategies

#### Basic physical protection

Basically, if the device holds sensitive data (e.g., credit cards, confidential documents), then keep it in a secure location.

Although, it might be problematic in real-world conditions, as people use smartphones for everything and anything, from entertainement to payments and administrative procedures.

#### Disable WPS

The WiFi Protected Setup can allow an attacker to access to the wireless network without entering any password. You should turn it off.

Otherwise, anyone who has physical access to the router can get on the network.

#### Rate limits

Some routers allow to prioritize specific traffic (e.g., WMM) and allocate bandwidth to a restricted list of devices and applications.

#### Pen-tests

We won't see pen-testing in details here, as this term is quite broad, but the idea with wireless pen-testing is to test wireless networks against known attacks regularly.

It's not highly expensive to create a rogue access point and a phishing page to see if the employees fall into the trap and give their credentials. You can leverage products like the [Wi-Fi Pineapple](https://www.wifipineapple.com/pages/software) to ease the setup.

Pen-testing distributions like Kali Linux also have pre-packaged utilities to sniff and hack wireless connections, starting with [detecting Hidden SSIDs](https://www.youtube.com/watch?v=7mQHmOZyY0Y&ab_channel=Packt).

## Other "not so uncommon" wireless technologies

While Wi-Fi and Bluetooth security may seem prevalent, Radio frequency identification (RFID), near field communication (NFC), and many other contactless technologies exist and have their own vulnerabilities.

Many systems rely on these technologies to store sensitive data, make payments, or unlock cars and hotel rooms. These information can be captured very discreetly, without the victim's knowledge or consent.

You can buy[^1] a [Flipper Zero](https://flipperzero.one/) and start hacking in the wild. This product is very comprehensive and costs around $200 (at the time of writing).

[^1]: I should probably not say that, as the product is sold-out at the time of writing, and Joom, the official reseller, "does not ship to the United States" ^^

## Is 4G secure?

Smartphones use a celullar connection, such as 4G or newer versions like LTE or 5G, to bring Internet access almost anywhere, as long as you receive the signal.

The **data is encrypted**, so decoding packets is not possible, theoretically. At least, it would be insanely challenging, like cracking the most robust cryptographic algorithms.

Don't get me wrong. Vulnerabilities can happen at higher level, for example, [this one in 2020](https://thehackernews.com/2020/02/lte-network-4g-vulnerability.html), but it remains pretty rare.

There are other angles of attack we won't see here, as these techniques require pretty advanced knowledge that are not in the scope of this introduction guide.

## What about IMSI-catchers?

An [IMSI-catcher](https://en.wikipedia.org/wiki/IMSI-catcher) is a special device used by authorities to intercept mobile phone traffic and exfiltrate other data. You cannot buy such product as an individual, at least, legally.

It can act as a fake cell tower to catch nearby phones. These attacks also exploit bugs in 4G modems and will likely require other vulnerabilities as prerequisites, for example, in the firmware. However, it's hardly documented, and if it's used againt you, reading this guide is not your top priority.

## 7 resources for beginners and intermediates

* [Hacktricks: pentesting WiFi](https://book.hacktricks.xyz/generic-methodologies-and-resources/pentesting-wifi)
* [A brief history of Wi-Fi security protocols from "oh my, that’s bad" to WPA3](https://arstechnica.com/gadgets/2019/03/802-eleventy-who-goes-there-wpa3-wi-fi-security-and-what-came-before-it/)
* [How to Hack Bluetooth Devices: 5 Common Vulnerabilities](https://hackernoon.com/how-to-hack-bluetooth-devices-5-common-vulnerabilities-ng2537af)
* [Rogue - deploy Access Points during penetration testing](https://github.com/InfamousSYN/rogue)
* [SANS - Enterprise Wireless Network Audit](https://www.sans.org/media/score/checklists/EnterpriseWirelessNetworkAudit.pdf)
* [CISA: Securing Networks for WiFi](https://www.cisa.gov/uscert/sites/default/files/publications/A_Guide_to_Securing_Networks_for_Wi-Fi.pdf)
* [NIST: Guide to Bluetooth security](https://www.nist.gov/publications/guide-bluetooth-security-2)
