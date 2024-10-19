# WEP/WPA Cracking

**Overview:** Analyzed vulnerabilities in wireless network protocols (WEP and WPA) by performing password-cracking attacks.

**Skills Developed:** Identifying MAC addresses and SSIDs, WEP/WPA password cracking, understanding network security flaws.

**Tools Used:** Wireshark, aircrack-ng, cowpatty, Kali Linux.

---

**Lab Details**

Introduction
	 Wireless network security is crucial in protecting data and maintaining privacy. WEP (Wired Equivalent Privacy) and WPA (Wi-Fi Protected Access) are two key protocols used to secure wireless networks, each with its own set of vulnerabilities and strengths. WEP was introduced in the late 1990s and is known for its weaknesses due to short key lengths and weak encryption mechanism making it susceptible to various attacks (Pereira, 2023). In contrast, WPA was developed to address WEP's shortcomings. It relies on stronger encryption and dynamic keys, although its effectiveness depends significantly on the chosen password's strength (Smith, 2022). Understanding how these protocols can be compromised is essential for improving wireless network security.

Objective
	The objective of this lab is to analyze wireless network security by performing password cracking attacks on WEP and WPA protocols. The lab will involve identifying key components such as Media Access Control (MAC) addresses and Service Set Identifiers (SSIDs) from capture files, using tools to crack WEP and WPA passwords, then documenting the process and findings. By comparing the effectiveness of these protocols and the methods used to exploit their vulnerabilities, individuals will gain insights into the importance of using a high valued security measures in wireless networks.	


Results and Analysis
	To begin this lab, the individual will open the Kali Linux machine then open Wireshark to examine the given pcap files. In Wireshark, the user will then have to go to File, then open, then where the user has saved the given pcap file. The first file to be examined is labeled ‘wep1.cap’. Using the filter ‘wlan.fc.type_subtype == 0x08’ the results are narrowed to one packet. After double clicking on this packet for further analysis the Media Access Control (MAC) address is found as ‘7c:8b:ca:cb:98:da’. This is under the source address in the packet or the source of the device that originated the frame. Within the same packet information will list the SSID parater set below. When the initial packet is clicked on to open the SSID parameter can be seen and somewhat made out at the bottom of the packet. The screenshot below will display the MAC address and the SSID parameter. 

 ![image](https://github.com/user-attachments/assets/c6609688-514b-4bcd-ab98-4d1f89df17e6)


  
	Next, using the filter ‘wlan.fc.type_subtype == 0x20’ this will display the beacon frames only in Wireshark. Then once the packets are displayed that are needed after filtering the other packets. The user will then focus on the source destination and the BS ID addresses. These display what addresses are ‘communicating’ with each other wirelessly. This can also be clarified by the 802.11 protocol Wireshark is displaying. The source is most likely an Alfa wireless adapter communicating to a Tp-Link router or modem. The screenshot below will display both MAC addresses in the screenshot. 

![image](https://github.com/user-attachments/assets/054b17de-6474-4335-bc0a-bd400a92b401)


  
Using aircrack-ng, a preinstalled Kali Linux tool for wireless password cracking. The user will type the command ‘aircrack-ng wep1.cap’. Since the username is located in the packet along with the MAC address and saved to the file, the tool just needs the file where it is saved. The following screenshot below is the output from aircrack-ng which displays ‘utica’ as the password to the MAC address of the BSS ID: 7c:8b:ca:cb:98:da. 

![image](https://github.com/user-attachments/assets/dbb2497c-0c1a-4a99-b166-082f0b46f0d0)


 
The next step is to open the pcap labeled ‘wep2.cap’. However, the user will follow the same previous steps as before. Using the same filter in Wireshark, ‘wlab.fc.type_subtype == 0x08’ only one packet will appear. Once the user double clicks on the packet to view more information. The individual will scroll down and view the source address as the MAC address given, ‘7c:8b:ca:cb:95:b4’ and the SSID parameter labeled “hackme4fun3”. The screenshot below displays both of these in Wireshark. 

![image](https://github.com/user-attachments/assets/16cf8734-6399-45fa-b3bd-58bd7bbb8ad2)

 
	Using the Wireshark filter, ‘wlan.fc.type_subtype == 0x20’ the user will then filter out any other packets other than the two devices communicating with each other. This can be verified by the 802.11 protocol in Wireshark. Once the user looks at any packet given, the user will want to look for the source address and the BSS ID addresses within the Wireshark packet. These can be displayed in the screenshot below. 

 ![image](https://github.com/user-attachments/assets/775a4b46-1513-4513-bebd-61a3a5682075)

 
Once this has been completed, the user will want to use aircrack-ng in Kali Linux to find the password for the MAC address in this pcap file. This will be done by executing the command ‘aircrack-ng wep2.cap’. This will take a couple of seconds longer, however, aircrack-ng will still find the password. The password is ‘utica’ again as the screenshot below shows. 

![image](https://github.com/user-attachments/assets/3ed2ef16-1c4f-401a-aed6-15a6f510fafe)

  
	The last file labeled ‘wpa.cap’ will be filtered using ‘wlan.fc.type_subtype == 0x08’. This will load one packet. Upon viewing this packet, the user can identify the Wireless Access Point (WAP) as the source destination and the SSID parameter. These both can be viewed in the screenshot below. 

 ![image](https://github.com/user-attachments/assets/69a16710-ea1b-44fd-88a3-d85706da86a5)

 
	In the next step, to find who this WAP is communicating with the user will type into Wireshark the filter ‘wlan.fc.type == 2’ this will display two MAC addresses or sources. The following screenshot will display both addresses. 

 ![image](https://github.com/user-attachments/assets/163cc146-d3e1-4cc0-b7dc-c11879e59ad9)

 
	Next, using aircrack-ng and the wordlist from github or that’s preinstalled in kali linux. The user will run the command ‘aricrack-ng -w /usr/share/wordlists/rockyou.txt wpa.cap’. If the user does not have the wordlist installed these can be found at github.com in the seclist repository. Then using the ‘git clone apt’ command the user can then install the wordlist into Kali linux to increase the number of password possibilities when cracking passwords. The following output from aircrack-ng is shown in the screenshot below. 

 ![image](https://github.com/user-attachments/assets/a9eae05b-6022-4c5b-859a-e659b13c13db)

	 
An additional way to crack the password of the ‘wpa.cap’ packet file is the use a tool called cowpatty. The command used is ‘cowpatty -r wpa.cap -f /usr/share/wordlists/rockyou.txt -s “hackme4fun1”. The tool will then display the command after a few moments as the screenshot below displays. 

![image](https://github.com/user-attachments/assets/380b2b65-fcf6-4318-965c-e940e81ccbc8)

 
	Wired Equivalent Privacy (WEP) and Wi-fi Protected Access (WPA) are wireless security protocols with specific vulnerabilities. WEP is an older protocol and is considered weak due to its short key lengths and predictable patterns. Attackers can crack WEP by capturing network traffic and analyzing it to determine the encryption key. However, WPA offers better security and relies heavily on the strength of the password. To crack WPA, attackers capture the 3-way handshake between a device and the access point, convert the file, then use tools to test various passwords until the correct one is found. Toos such as aircrack-ng, hashcat, and cowpatty, are commonly used for these attacks displaying the importance of strong passwords within networks and infrastructure. 


Conclusion
	 This lab provided practical experience in analyzing and cracking wireless network security by focusing on WEP and WPA protocols. Individuals learned how to identify network components like MAC addresses and SSIDs then used a wireless network tool to attack these protocols. The lab demonstrated WEP's weaknesses, such as its short key lengths and vulnerability to attack. In contrast, WPA's security depends on the strength of the password, displaying the importance of using strong passphrases. By cracking WPA passwords with tools like aircrack-ng and cowpatty, users saw firsthand the need for strong security practices to protect wireless networks.
