## Unit 19 Homework: Protecting VSI from Future Attacks

### Scenario

In the previous class,  you set up your SOC and monitored attacks from JobeCorp. Now, you will need to design mitigation strategies to protect VSI from future attacks. 

You are tasked with using your findings from the Master of SOC activity to answer questions about mitigation strategies.

### System Requirements 

You will be using the Splunk app located in the Ubuntu VM.

### Logs

Use the same log files you used during the Master of SOC activity:

- [Windows Logs](resources/windows_server_logs.csv)
- [Windows Attack Logs](resources/windows_server_attack_logs.csv)
- [Apache Webserver Logs](resources/apache_logs.txt	)
- [Apache Webserver Attack Logs](resources/apache_attack_logs.txt	)

---

### Part 1: Windows Server Attack

Note: This is a public-facing windows server that VSI employees access.
 
#### Question 1
- Several users were impacted during the attack on March 25th.
- Based on the attack signatures, what mitigations would you recommend to protect each user account? Provide global mitigations that the whole company can use and individual mitigations that are specific to each user.

- Global Solution: The best global mitigation would probably be to add multi-factor authentication to the companies systems. This would greatly reduce the number of successes of a threat actor to access user accounts.

-Individual Solutions:
User_K: An Attempt was made to reset an account password. While logs suggest that attacker was unsuccessful in reseting the password for user_k. The attempt to reset the password has been made several times. The best mitiagation for this user would be to set up user-specific alerts with lower values in order to more closely analyze and watch for the users password getting changed again

User_A: User account was locked out.
Suggestions for User_A is to change their password immediately to something completely different and ensure that the password complexity is high. This is because the attacker is trying to brute force their way to the users password in order to steal the account

User_J: An account was successfully logged on
The log shows that the attacker was able to successfully obtain the users password
The best thing to do is to change the password for User_J manually and to use the same mitigation tactic as used for User_K
![Screenshot (150)](https://user-images.githubusercontent.com/89820505/154904060-1977b6f7-7d31-4bfb-a82a-250a9ad987f6.png)
![Screenshot (151)](https://user-images.githubusercontent.com/89820505/154904078-f9e83453-3324-4b8a-854d-da7ec74d40de.png)

  
#### Question 2
- VSI has insider information that JobeCorp attempted to target users by sending "Bad Logins" to lock out every user.
- What sort of mitigation could you use to protect against this?
 Easiest solution would be to set up a group policy for the company.
 That group policy would automatically unlock users accounts after a set amount of time. As soon as the company finds out about this insider attack, the employees should also be notified immediately to be more vigilant & careful about who they accept information from

### Part 2: Apache Webserver Attack:

#### Question 1
- Based on the geographic map, recommend a firewall rule that the networking team should implement.
- Provide a "plain english" description of the rule.
  - For example: "Block all incoming HTTP traffic where the source IP comes from the city of Los Angeles."
- Provide a screen shot of the geographic map that justifies why you created this rule. 
Most of the incoming attacks were coming from Ukraine. Therefore we should set up a firewall rule to block HTTP traffic from Ukraine. Firewall rule should describe "Block all incoming HTTP traffic where the source IP comes from the country of Ukraine"
![Screenshot (152)](https://user-images.githubusercontent.com/89820505/154905258-a2d9b3ae-2de5-4227-a27f-521e82dff473.png)
![Screenshot (153)](https://user-images.githubusercontent.com/89820505/154905278-3df6c40d-9f9d-4833-9dec-cbcd9efa65ee.png)

  
#### Question 2

- VSI has insider information that JobeCorp will launch the same webserver attack but use a different IP each time in order to avoid being stopped by the rule you just created.

- What other rules can you create to protect VSI from attacks against your webserver?
  - Conceive of two more rules in "plain english". 
  - Hint: Look for other fields that indicate the attacker.
You can create two other rules based off of "user_agent" & "bytes".
Both rules should go as followed:
Block all incoming HTTP traffic where the useragent is "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.2; SV1; .NET CLR 2.0.50727987787; InfoPath.1)."
Block all incoming HTTP traffic where the bytes amount is 65748"


### Guidelines for your Submission:
  
In a word document, provide the following:
- Answers for all questions.
- Screenshots where indicated

Submit your findings in BootCampSpot!

---

© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.
