# Day 11[Wi-Fi Attacks]: If you'd like to WPA, press the star key!

## Story :
Glitch and McSkidy find out that the mayor could still get into their networks by exploiting the WiFi access points. Let us check if the warevilles Wifi could be easily accessed for malicious purposes by checking different existing methods. 

## Learning Objecctives : 
- Understand what Wi-Fi is
- Explore its importance for an organisation
- Learn the different Wi-Fi attacks
- Learn about the WPA/WPA2 cracking attack

## Abbreviations and Applications :
- [Wi-Fi](https://www.cisco.com/c/en_in/products/wireless/what-is-wifi.html) : Wi-Fi is a wireless networking technology that allows devices such as computers (laptops and desktops), mobile devices (smart phones and wearables), and other equipment (printers and video cameras) to interface with the Internet. Contrary to the common mis-conception it is not an acronym for Wireless-Fidelity, thought it has been used in some places.
- [AP](https://www.cisco.com/c/en/us/solutions/small-business/resource-center/networking/what-is-access-point.html#~types-of-access-points) : A wireless access point (WAP) is a networking device that allows wireless-capable devices to connect to a wired network.
- [SSID](https://nordvpn.com/blog/what-is-ssid/) : SSID stands for “service set identifier” and is your Wi-Fi network name.
- [BSSID](https://www.atera.com/blog/computer-terms-unwrapped-what-is-bssid/) : BSSID stands for Basic Service Set Identifier.
- [PSK](https://doctorengenius.engeniustech.com/en/articles/6708681-what-is-a-pre-shared-key-psk) : Pre-Shared Key.
- [WPS](https://us.hitrontech.com/learn/what-is-wps-on-my-router/) : WiFi Protected Setup. A router with a WPS button can allow any device to automatically connect to your router when the WPS button is pressed.
- [WPA/WPA2](https://www.arubanetworks.com/techdocs/InstantWenger_Mobile/Advanced/Content/Instant%20User%20Guide%20-%20volumes/Understanding_WPA_and_WP.htm) : Wi-Fi Protected Access 2 (WPA2) is the final version of WPA agreed on by the Wi-Fi Alliance; it implements all aspects of the ratified 802.11i security standard and is mandatory in the Wi-Fi certification process. WPA2 is backward-compatible with WPA and can be implemented in two versions — WPA2 personal and WPA2 enterprise.

## Process Key Steps and Points :

**Some Types of WiFi Attacks:**
* **Evil twin attack**: In this attack, the attacker creates a fake Wi-Fi access point with a similar name to one of your trusted access points. For instance, if your trusted Wi-Fi’s name is “Home_Internet,” the attacker creates a fake Wi-Fi access point named “Home_Internnet” or something similar that’s hard to distinguish. The attack begins with the attacker sending de-authentication packets to all users connected to their legitimate Wi-Fi access points. As a result, users will experience repeated disconnections from the network. Frustrated, they’ll likely open their Wi-Fi access points list for troubleshooting and discover the attacker’s Wi-Fi with a similar name and stronger signal strength. They’ll connect to it, and the attacker can then intercept all their internet traffic.
* **Rogue access point**: This attack aims to achieve the same objective as the evil twin attack. The attacker sets up an open Wi-Fi access point near or within the organization’s physical premises to make it accessible to users with good signal strength. If users’ devices are set to automatically connect to open Wi-Fi, they may inadvertently join this network. Once connected, the attacker can intercept all their communication.
* **WPS attack**: Wi-Fi Protected Setup (WPS) was designed to simplify the process of connecting to Wi-Fi networks by requiring users to remember only an 8-digit PIN. However, this PIN can be vulnerable in certain networks due to its insecure configuration. The attack involves initiating a WPS handshake with the router and capturing the router’s response, which contains sensitive information related to the PIN. This information can be vulnerable to brute-force attacks, and the PIN can be successfully extracted along with the Pre-Shared Key (PSK).
* **WPA/WPA2 Cracking**: Wi-Fi Protected Access (WPA) was introduced to secure wireless communication using a robust encryption algorithm. However, its security heavily relies on the length and complexity of the Pre-Shared Key (PSK).Cracking WPA involves sending de-authentication packets to a legitimate user of the Wi-Fi network. Once the user disconnects, the attacker attempts to reconnect to the network. During this process, a 4-way handshake with the router occurs. Simultaneously, the attacker switches their adaptor to monitor mode and captures the handshake.
  After capturing the handshake, the attacker can exploit it by employing brute-force or dictionary attacks on the captured handshake file.

### The 4-way Handshake :
The WPA 4-way handshake is a crucial process that enables a client device (such as a smartphone or laptop) and a Wi-Fi router to authenticate and establish a secure connection. Here's a simplified breakdown of the process:

1. **Authentication Request**: The router sends an authentication request, known as a challenge, to the client. This challenge is essentially a request for the client to prove its knowledge of the network's password without directly sharing it.
2. **Encrypted Response**: The client receives the challenge and uses the Pre-Shared Key (PSK) to encrypt a response. This encrypted response is then sent to the router, which can verify its authenticity only if it possesses the correct PSK.
3. **Verification and Confirmation**: If the router verifies the client's response, it sends a confirmation back to the client. This confirmation serves as a mutual agreement between the client and router that they both possess the correct PSK.
4. **Secure Connection Establishment**: The client verifies the router's response, and upon successful authentication, they establish a secure connection. The WPA 4-way handshake ensures that the PSK remains secure, as it is never directly revealed during the authentication process.

### Now the process followed for WPA2 cracking :
> 1. Scan and find out the wireless device details and the network to gain access to.
> 2. Launch a deauthentication attack on a device connected to the target AP.
> 3. Set our device into monitor mode and capture the 4-way handshake of the target device and target AP.
> 4. Brute-Force Crack the PSK and gain access.

## Tools and Commands used :
* `iw dev` : This will show any wireless devices and their configuration that we have available for us to use.
* `sudo iw dev dev_name scan` : To scan for wireless networks using the device with name dev_name.
* `sudo ip link set dev dev_name up(down)` : To turn on(off) the device.
* `sudo iw dev dev_name set type monitor(managed)` : Change the mode of the wireless device.
* `sudo airodump-ng -c 6 --bssid bssid -w output-file dev_name` : This command targets the specific network channel and MAC address (BSSID) of the access point for which you want to capture the traffic and saves the information to a few files that start with the name output-file.
* `sudo aireplay-ng -0 1 -a AP_bssid -c client_bssid dev_name` : Deauthentication attack, -0 flag indicates that we are using the deauthentication attack, and the 1 value is the number of deauths to send. 
* `sudo aircrack-ng -a 2 -b AP_bssid -w wordlist.txt output*cap` : Brute Force cracking with a wordlist dictionary file, where the -a 2 flag indicates the WPA/WPA2 attack mode and -w flag indicates the dictionary list to use for the attack.
* `wpa_passphrase AP_ssid 'ENTER PSK HERE' > config && sudo wpa_supplicant -B -c config -i dev_name` : To connect to an AP with AP_ssid and and PSK.

## Questions, Hints and Answers :
1. What is the BSSID of our wireless interface?
   * Hint : Use `iw dev`
   * Ans : 02:00:00:00:02:00
2. What is the SSID and BSSID of the access point? Format: SSID, BSSID
   * Hint : Use `sudo iw dev dev_name scan`
   * Ans : MalwareM_AP, 02:00:00:00:00:00
3. What is the BSSID of the wireless interface that is already connected to the access point?
   * Hint : Use `airodump-ng`
   * Ans : 02:00:00:00:01:00
4. What is the PSK after performing the WPA cracking attack?
   * Hint : Check the directory of the wordlist properly.
   * ![PSK_WiFi](/Screenshots/D11Q4.png)
   * Ans : fluffy/champ24

