# SOAR EDR Project

## Objective

The SOAR EDR project was geared to design an environment for automatic detection and responses. The primary focus was to create a SOAR playbook using various automation tools, respond to security events as they happen automatically, and perform actions based on user responses to events. This project aimed to gain a deeper understanding of certain processes that could be automated in the real world, create rules and user prompts for detection, and obtain hands-on experience in setting up a SOAR environment.

### Skills Learned

- Advanced understanding of SOAR concepts and practical application.
- Learned how to create virtual hosts and configure automation software.
- Gained an understanding of how certain components are connected for automation using application channels, sensors, outputs, and webhooks.
- Ability to create detection and response rules for SOAR environment.
- Created a SOAR environment using Tines.
- Configure the process to isolate machines automatically after a security event is detected.
- Ability to send detection and response alerts through emails or to a shared community channel automatically.

### Tools Used

- Endpoint detection and analysis software. // LimaCharlie
- Shared community channel for alerts and responses. // Slack
- Virtual environment for target endpoint machine. // VMWare
- SOAR environment software. // Tines

## Steps
![Soar EDR](https://github.com/user-attachments/assets/4ae08e92-286b-4604-abf0-9b682492b1a1)
1. Created a Windows 10 Pro Virtual Machine, and installed LimaCharlie (endpoint detection and analysis software) using the provided installer and installation key.
2. Downloaded the Hack Tool Lazagne.exe from Github repository to start generating test security events on the Windows 10 Pro Machine. 
3. On LimaCharlie I navigated to the D&R rules and searched for a new process creation credential access rule. Modified the raw code by replacing the value with Lazagne.exe to start detecting all processes created by Lazagne.exe. I also included a command line rule for all instances mentioning Lazagne.exe in the comamnd line.<br>
<br> ![Screenshot 2024-09-27 063127](https://github.com/user-attachments/assets/65c0e5ea-5405-4824-be1c-e8fb9a6a6165)
5. Tested the detection on LimaCharlie by running the Lazagne.exe executable. Confirmed that the endpoint was able to detect security events to LimaCharlie. <br>
<br>![Screenshot 2024-09-27 064423](https://github.com/user-attachments/assets/a9add8dd-f1d1-42fa-8375-53d58454efc2)
6. Created a community channel on Slack, to correlate all alerts to one software.
7. On Tines, I created a new story starting with a webhook URL to our LimaCharlie software. By this process, I was able to connect Tines with detection events from LimaCharlie.
8. Using the above diagram, I imported the appropriate Slack and Email modules to send alerts once events were detected.
9. I connected the Slack module by copying the channel code to the Tines playbook, as well as providing my own personal email into the email module.
10. For the message, I included the same message that was provided in the above diagram to the Slack and email modules.
11. I imported a user prompt page, for the user to respond to the alert. Provided a "Do you want to isolate this machine?" message with a boolean input field (yes/no).
12. By using the event details in Tines. I was also able to include the host's details on the alert messages as well, that way the receiving user will also be notified of the specific system details the alert originated from. <br>
<br> ![Screenshot 2024-09-30 232114](https://github.com/user-attachments/assets/ea25faf3-c1b7-44a0-8a29-19592882257b)
13. I added a new credential of LimaCharlie to the Tines environment with the LimaCharlie API key.
14. Added triggers to the user prompt page, with actions to take when a user selects both "yes" or "no"
15. For "No" I sent a message to Slack confirming the machine was not isolated. For "yes" I connected a LimaCharlie module with the action "Isolate Sensor" and chose to connect it with the appropriate sensor ID.
16. I generated the test event on my Windows 10 Pro VM, confirmed the messages were sent to both Slack and my email, and selected "Yes" on the user prompt page. I then confirmed that the machine was isolated on LimaCharlie.
![Screenshot 2024-09-28 230957](https://github.com/user-attachments/assets/6ae97df1-65e7-404a-9352-b103af3fbcf1)
![Screenshot 2024-09-28 233355](https://github.com/user-attachments/assets/9dd97f5f-5d83-4c14-9780-6f9137dbdd98)
![Screenshot 2024-10-01 010115](https://github.com/user-attachments/assets/05c7791b-9d52-4e9f-b907-2485a9674612)
![Screenshot 2024-09-30 234211](https://github.com/user-attachments/assets/4bd46a6e-4f0f-4d46-8554-5a941950647c)


