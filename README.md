# Net-Sec-Challenge-Writeup

Net Sec Challenge Writeup (TryHackMe) By King 

TryHackMe Difficulty Rating: Medium

Net Sec Challenge is a VIP room on TryHackMe that can help you test your network security skills using Nmap, Telnet, and Hydra.

![netsec0](https://github.com/MRKING20/Net-Sec-Challenge-Writeup/assets/64786452/90b4447a-b67e-4f9c-b01a-dc3bf39aa90b)

Room Link: https://tryhackme.com/room/netsecchallenge

Task 1: Introduction 

Task 2: Challenge Questions 

![netsec1](https://github.com/MRKING20/Net-Sec-Challenge-Writeup/assets/64786452/8a604937-f65d-4b5c-929a-698aff282666)

Q1: What is the highest port number being open less than 10,000?

We are going to use Nmap to scan our target machine for open ports with this command:  $ sudo nmap MACHINE_IP

![Q1](https://github.com/MRKING20/Net-Sec-Challenge-Writeup/assets/64786452/3a224dea-1f75-4ac3-b04f-daa614bf4b92)

Q2 + Q3:  We need now to scan for all the ports to be able to answer these questions. As a result, the scan may take several minutes or more. 

Our is command: $ sudo nmap -p- -T4 MACHINE_IP -v  (or -p-:scans all the ports, -T4: for faster scan and -v: for verbose 

![Q2 Q3 2](https://github.com/MRKING20/Net-Sec-Challenge-Writeup/assets/64786452/dcbe6ed1-fcbc-463c-9068-db4b97db5658)

Q4 + Q5: we need to use this command $ sudo nmap -sS -A  MACHINE_IP (or -sS: for TCP SYN Scan and -A: eq to -sV -O -sC --traceroute where -sV: determine service/version info on open ports, -O: detect OS, -sC: run default scripts and --traceroute: run traceroute to target)

![Q4 Q5](https://github.com/MRKING20/Net-Sec-Challenge-Writeup/assets/64786452/6d59c826-2efc-4945-8872-35415f4bdd00)

Q6: we know that the FTP server is listening on a nonstandard port "Port 21 is wrong" so I tried port number 10021 which has an unknown service 

Our is command: $ ftp 10.10.154.144 10021

![Q6](https://github.com/MRKING20/Net-Sec-Challenge-Writeup/assets/64786452/f97c0ae1-90e1-48cf-9db8-d50dc47b313e)

Q7: We learned two usernames using social engineering: eddie and quinn. To get the flag hidden in one of these two account files, first of all, we need to save these usernames to a file. Then we will use Hydra and /usr/share/wordlists/rockyou.txt file to figure out their passwords.

step 1: $ hydra -l eddie -P /usr/share/wordlists/rockyou.txt 10.10.154.144 ftp -vV -d -s10021 (to find the pass of eddie)
step 2: $ hydra -l quinn -P /usr/share/wordlists/rockyou.txt 10.10.154.144 ftp -vV -d -s10021 (to find the pass of quinn)

-l: Provide the login name
-P: Loads several passwords from a file 
-vV: Show the username and password combinations being tried
-d: Debugging the output
-s: For specific port

After finding the passwords we need to connect and get the flag: 

![Q7](https://github.com/MRKING20/Net-Sec-Challenge-Writeup/assets/64786452/bc79f796-fbcf-497a-bbf3-a2708e5a85b3)

Q8: To answer the last question of the challenge we need to visit http://MACHINE_IP:8080.

To reduce the probability of being detected, we are going to run a NULL scan using Nmap. As you might remember, the null scan does not set any flag. And by sending requests which do not include the SYN flag, we can bypass the firewall.

Our command is : $ sudo nmap -sN MACHINE_IP (-sN: for Null Scan)

![Q8](https://github.com/MRKING20/Net-Sec-Challenge-Writeup/assets/64786452/aee69fc6-3763-4f5f-a1df-d1ba5c7260f9)
The flag appeared instantly after I hit enter to run the scan. Task completed 🙂

Note: If it doesn't work from your local machine, try running nmap on the AttackBox. :)


/////////////////////////THE END\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\

I hope this write-up helped you to complete this challenge 

!! HAPPY LEARNING !!


