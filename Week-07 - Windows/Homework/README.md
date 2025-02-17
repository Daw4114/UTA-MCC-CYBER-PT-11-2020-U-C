## Week 7 Homework: A Day in the Life of a Windows Sysadmin

### Overview  

This homework assignment builds on the Group Policy Objectives activities from the previous class.  We will create domain-hardening GPOs and revisit some PowerShell fundamentals.

:warning: The Day 3 activities must be fully completed in order to complete this activity. If they are not, you will need to refer to your student guides and set up your domain OUs, users, and groups.

### Lab Environment

For this week's homework, please use the Windows Server machine and Windows 10 machine inside your Azure Windows RDP Host machine. 

**Windows RDP Host Machine:**
  - Username: `azadmin`
  - Password: `p4ssw0rd*`

Open the Hyper-V Manager in the Windows RDP Host machine to access the nested virtual machines:

**Windows 10 Machine**
  - Username: `sysadmin`
  - Password: `cybersecurity`

**Windows Server Machine:**
  - Username: `sysadmin`
  - Password: `p4ssw0rd*`

**Note**: The instructions for each task will tell you which machine to work in.

The following document contains a list of Windows issues that commonly occur during this unit. Familiarize yourself with these issues so you can fix them as needed:

- [Understanding the Windows Unit Lab](https://docs.google.com/document/d/18Mz12q82nhxkypVRdIVgIqsLeNG1oCQj_TPsFJ3RgGk/edit)

Refer to your Unit 7 Student Guides if you have trouble with this homework.

---

### Task 1: Create a GPO: Disable Local Link Multicast Name Resolution (LLMNR)

For this first task, you will investigate and mitigate one of the attack vectors that exists within a Windows domain.

- [Read about LLMNR vulnerabilities in the the MITRE ATT&CK database](https://attack.mitre.org/techniques/T1171/). 

   - MITRE is one of the world's leading organizations for threat intelligence in cybersecurity. 

   - MITRE maintains the Common Vulnerabilities and Exposures database, which catalogs officially known exploits.
 
   - It also maintains this MITRE ATT&CK database, which catalogs attack methods and signatures of known hacking groups.

**Local Link Multicast Name Resolution (LLMNR)** is a vulnerability, so we will be disabling it on our Windows 10 machine (via the `GC Computers` OU). 

A few notes about LLMNR:

- LLMNR is a protocol used as a backup (not an alternative) for DNS in Windows. 

- When Windows cannot find a local address (e.g. the location of a file server), it uses LLMNR to send out a broadcast across the network asking if any device knows the address. 

- LLMNR’s vulnerability is that it accepts any response as authentic, allowing attackers to poison or spoof LLMNR responses, forcing devices to authenticate to them. 

- An LLMNR-enabled Windows machine may automatically trust responses from anyone in the network.

Turning off LLMNR for the `GC Computers` OU will prevent our Windows machine from trusting location responses from potential attackers.

#### Instructions

Since this task deals with Active Directory Group Policy Objects, you'll be working in your nested **Windows Server** machine.

Create a Group Policy Object that prevents your domain-joined Windows machine from using LLMNR:

1. On the top-right of the Server Manager screen, open the Group Policy Management tool to create a new GPO.

2. Right-click **Group Policy Objects** and select **New**.

3. Name the Group Policy Object `No LLMNR`.

4. Right-click the new **No LLMNR** GPO listing and select **Edit** to open the Group Policy Management Editor and find policies.

5. In the Group Policy Management Editor, the policy you are looking for is at the following path: `Computer Configuration\Policies\Administrative Templates\Network\DNS Client`.

    - Find the policy called `Turn Off Multicast Name Resolution`.

    - Enable this policy.

6. Exit the Group Policy Management Editor and link the GPO to the `GC Computers` organizational unit you previously created.

---

### Task 2: Create a GPO: Account Lockout

For security and compliance reasons, the CIO needs us to implement an account lockout policy on our Windows workstation. An account lockout disables access to an account for a set period of time after a specific number of failed login attempts. This policy defends against brute-force attacks, in which attackers can enter a million passwords in just a few minutes.

Account lockouts have some important considerations. Read about these in the following documentation:
- [Microsoft Security Guidance: Configuring Account Lockout](https://docs.microsoft.com/en-us/archive/blogs/secguide/configuring-account-lockout) 
- You only need to read the "Account Lockout Tradeoffs" and "Baseline Selection" sections.

To summarize, an overly restrictive account lockout policy (such as locking an account for 10 hours after 2 failed attempts), can potentially keep an account locked forever if an attacker repeatedly attempts to access it in an automated way.

#### Instructions

You'll be working within in your nested Windows Server machine again to create another Group Policy Object.

Create what you believe to be a reasonable account lockout Group Policy for the Windows 10 machine. 

1. Name the Group Policy Object `Account Lockout`.

2. You can use Microsoft's 10/15/15 recommendation if you'd like.

3. When editing policies for this new GPO, keep in mind that you're looking for _computer configuration_ policies to apply to your `GC Computers` OU. Also, these policies involve Windows _security settings_ and _accounts_.

4. Don't forget to link the GPO to your `GC Computers` organizational unit.

**Hint**: If you're confused about where to find the right policies, check the instructions in italics.

---

### Submission Guidelines

Provide the following:

- **Deliverable for Task 1:** Take a screenshot of all the GPOs created for this homework assignment. To find these, launch the Group Policy Management tool, select **Group Policy Objects**, and take a screenshot of the GPOs you've created.

- **Deliverable for Task 2:** Submit a screenshot of the different `Account Lockout` policies in Group Policy Management Editor. It should show the three values you set under the Policy and Policy Setting columns.

© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.
