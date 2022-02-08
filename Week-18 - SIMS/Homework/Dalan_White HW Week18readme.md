## Unit 18 Homework: Lets go Splunking!

### Scenario

You have just been hired as an SOC Analyst by Vandalay Industries, an importing and exporting company.
 
- Vandalay Industries uses Splunk for their security monitoring and have been experiencing a variety of security issues against their online systems over the past few months. 
 
- You are tasked with developing searches, custom reports and alerts to monitor Vandalay's security environment in order to protect them from future attacks.


### System Requirements 

You will be using the Splunk app located in the Ubuntu VM.


### Your Objective 

Utilize your Splunk skills to design a powerful monitoring solution to protect Vandaly from security attacks.

After you complete the assignment you are asked to provide the following:

- Screen shots where indicated.
- Custom report results where indicated.

### Topics Covered in This Assignment

- Researching and adding new apps
- Installing new apps
- Uploading files
- Splunk searching
- Using fields
- Custom reports
- Custom alerts

Let's get started!

---

## Vandalay Industries Monitoring Activity Instructions


### Step 1: The Need for Speed 

**Background**: As the worldwide leader of importing and exporting, Vandalay Industries has been the target of many adversaries attempting to disrupt their online business. Recently, Vandaly has been experiencing DDOS attacks against their web servers.

Not only were web servers taken offline by a DDOS attack, but upload and download speed were also significantly impacted after the outage. Your networking team provided results of a network speed run around the time of the latest DDOS attack.

**Task:** Create a report to determine the impact that the DDOS attack had on download and upload speed. Additionally, create an additional field to calculate the ratio of the upload speed to the download speed.


1.  Upload the following file of the system speeds around the time of the attack.
    - [Speed Test File](resources/server_speedtest.csv)

2. Using the `eval` command, create a field called `ratio` that shows the ratio between the upload and download speeds.
   - Hint: The format for creating a ratio is: `| eval new_field_name = 'fieldA'  / 'fieldB'`
      
3. Create a report using the Splunk's `table` command to display the following fields in a statistics report:
    - `_time`
    - `IP_ADDRESS`
    - `DOWNLOAD_MEGABITS`
    - `UPLOAD_MEGABITS`
    - `ratio`
  
   Hint: Use the following format when for the `table` command: `| table fieldA  fieldB fieldC`

4. Answer the following questions:

    - Based on the report created, what is the approximate date and time of the attack?
    - On 02-23-2020 14:30. An Attack took place where the download megabit speed had drastically decreased from 109.16 MPS to 7.87 MPS
    - How long did it take your systems to recover?
    Lasted till 02-23-2020 23:30 where speeds returned to 122.91 MPS
    - [Screenshot (137)](https://user-images.githubusercontent.com/89820505/152834128-3a99243a-bf51-4cfa-8e01-a8c59c8c4ecb.png)
    
![Screenshot (138)](https://user-images.githubusercontent.com/89820505/152834211-1721059e-ec1e-4847-9410-4f7bfb30554b.png)


Submit a screen shot of your report and the answer to the questions above.
 
### Step 2: Are We Vulnerable? 

**Background:**  Due to the frequency of attacks, your manager needs to be sure that sensitive customer data on their servers is not vulnerable. Since Vandalay uses Nessus vulnerability scanners, you have pulled the last 24 hours of scans to see if there are any critical vulnerabilities.

  - For more information on Nessus, read the following link: https://www.tenable.com/products/nessus

**Task:** Create a report determining how many critical vulnerabilities exist on the customer data server. Then, build an alert to notify your team if a critical vulnerability reappears on this server.

1. Upload the following file from the Nessus vulnerability scan.
   - [Nessus Scan Results](resources/nessus_logs.csv)

2. Create a report that shows the `count` of critical vulnerabilities from the customer database server.
   - The database server IP is `10.11.36.23`.
   - The field that identifies the level of vulnerabilities is `severity`.
      
3. Build an alert that monitors every day to see if this server has any critical vulnerabilities. If a vulnerability exists, have an alert emailed to `soc@vandalay.com`.
![Screenshot (140)](https://user-images.githubusercontent.com/89820505/152929691-d15f2799-cec2-4fb4-b370-0337e9722b4f.png)

![Screenshot (141)](https://user-images.githubusercontent.com/89820505/152931062-3c2c6dc3-408a-47db-88fd-12c57a500e93.png)

Submit a screenshot of your report and a screenshot of proof that the alert has been created.


### Step 3: Drawing the (base)line

**Background:**  A Vandaly server is also experiencing brute force attacks into their administrator account. Management would like you to set up monitoring to notify the SOC team if a brute force attack occurs again.


**Task:** Analyze administrator logs that document a brute force attack. Then, create a baseline of the ordinary amount of administrator bad logins and determine a threshold to indicate if a brute force attack is occurring.

1. Upload the administrator login logs.
   - [Admin Logins](resources/Administrator_logs.csv)

2. When did the brute force attack occur?
   - Hints:
     - Look for the `name` field to find failed logins.
     - Note the attack lasted several hours.

      
3. Determine a baseline of normal activity and a threshold that would alert if a brute force attack is occurring.!
Looking at the 'name' field for "An account failed to log on" I was able to look & determine the time of attack.
the brute force attack occured from 9:00 until 14:00 on 02/21/2020 for a total of 5 hours
Standard baseline is 5 to 35 logs an hour. The threhold shouldbe set at 40 or more login attempts in an hour and the alert will be sent to SOC@vandalay.com when triggered
[Screenshot (142)](https://user-images.githubusercontent.com/89820505/152935429-2ca8f9c3-53ad-47da-b636-c28bc50ea314.png)


4. Design an alert to check the threshold every hour and email the SOC team at SOC@vandalay.com if triggered. ![Screenshot (143)](https://user-images.githubusercontent.com/89820505/152936030-67831615-478f-4eb1-ad71-46b35b83cf02.png)



Submit the answers to the questions about the brute force timing, baseline and threshold. Additionally, provide a screenshot as proof that the alert has been created.
 
 
### Your Submission
  
In a word document, provide the following:
  - Answers to all questions where indicated. 
  - Screenshots where indicated.

---

© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.
