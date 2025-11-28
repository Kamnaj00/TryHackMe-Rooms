/Room: Introduction to Cyber Security

Task 1 – Offensive Security
Question: Which of the following options better represents the process where you simulate a hacker's actions to find vulnerabilities in a system?  
- Offensive Security  
- Defensive Security  

Correct Answer: Offensive Security ✅  

Key Notes:  
- Offensive Security = simulating hacker tactics to identify weaknesses.  
- Purpose: strengthen defenses by understanding how attacks work.  
- Ethical hackers use these methods legally to protect organizations.


Task 2 – Hacking Your First Machine
Objective: Use Gobuster to discover hidden directories on the FakeBank application.  

Steps Taken:  
1. Opened terminal in the TryHackMe VM.  
2. Ran command:  
   ```bash
   gobuster -u http://fakebank.thm -w wordlist.txt dir

3. Discovered hidden directories:

/images
/bank-transfer (Status: 200 → accessible page)

4. Navigated to /bank-transfer in browser.
5. Transferred $2000 from account 2276 to account 8881.
6. Verified new balance on account page.

Correct Answer: BANK-HACKED ✅ 

Outcome:

Successfully exploited hidden functionality.
Learned how directory brute-forcing can reveal sensitive admin pages.
Reinforced importance of securing web applications against misconfigurations.

Task 3 – Careers in Cyber Security
Key Takeaways:

Cybersecurity careers can be offensive (attacking) or defensive (protecting).

Examples of offensive roles:

Penetration Tester – tests systems for exploitable vulnerabilities.
Red Teamer – simulates adversary attacks to assess resilience.
Security Engineer – designs and maintains security controls.
Path to learning: practice daily, document progress, build hands-on skills.

Correct Answer: No Answer needed ✅

Skills Practiced

- Offensive Security fundamentals
- Directory brute-forcing with Gobuster
- Web application vulnerability discovery
- Understanding cybersecurity career paths
