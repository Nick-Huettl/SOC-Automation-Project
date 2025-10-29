# 🛡️ SOC Automation Project 🛡️

As AI becomes more prevalent in cybersecurity operations, I wanted to explore the idea of how automation could assist in a Security Operations Center (SOC) environment.
This project simulates a small SOC setup & demonstrates how tools like Splunk, n8n, OpenAI, and Slack can work together to detect, analyze, and automatically respond to security events.

This project was inspired by the following video:
https://www.youtube.com/watch?v=Xh9AP-x06jU

## Tools Used

- VMWare Workstation - Windows 11 25H2 / Ubuntu
- Splunk
- n8n
- OpenAI
- Slack

## Project Objectives

- Create virtual machines, including a Windows 11 machine & 2 Ubuntu servers to simulate a SOC Environment.
- Install Splunk & n8n on the Ubuntu machines.
- Configure Splunk to receive telemetry & logs from the Windows 11 machine.
- Set up communication between Splunk & n8n to automate workflows based on alerts.
- Integrate OpenAI into n8n to generate responses to simulated attacks.
- Send the AI-generated responses & alerts to Slack.

### Windows 11 VM

The initial setup included downloading VMware Workstation and creating the virtual machines that would be needed for the project. I started with the Windows 11 machine, as this will be the machine that sends its telemetry and logs over to Splunk.

<img width="1919" height="1075" alt="VMsetupComplete" src="https://github.com/user-attachments/assets/ca6c1309-6d02-49bf-9391-120e30aab775" />

After the Windows 11 machine was downloaded and running, I created a snapshot in case anything were to happen, so that the base Windows 11 machine could be restored if needed. 

### Splunk on Ubuntu

I then moved on to the Ubuntu server that would host Splunk. This was done by using the command line on Ubuntu and using the wget link provided on Splunk's site after creating an account.

Once installed, I could go over to my host machine's browser and enter the Ubuntu VM's IP address and the port 8000 (Splunk's default web interface port) to reach the Splunk interface and sign in.

<img width="1640" height="938" alt="SplunkInstalledUbuntu" src="https://github.com/user-attachments/assets/f2ee9743-ac68-403d-aef4-57541504d287" />

### Configuring Splunk & Forwarder

With Splunk up, I created a new index to eventually display the Windows 11 telemetry and logs.

To connect the Windows 11 VM and the Splunk instance, I downloaded and installed the Splunk Universal Forwarder. This allows the logs and telemetry to be sent over to Splunk once configured properly. 

<img width="1915" height="974" alt="VMForwardingTelemetrySplunk" src="https://github.com/user-attachments/assets/bf5fb0ae-7552-4019-92db-8e1cf5b0c1d5" />

### Testing Log Forwarding

Now that Splunk is receiving the telemetry and logs, I tested to ensure that Splunk would receive the brute force attack attempt. 

This was done by attempting several failed RDP logins into the Windows 11 machine. 

 I verified these events by using the 'EventCode=4625' query to narrow the logs down to unsuccessful Window logon attempts.

<img width="1713" height="903" alt="FailedAttemptsRDPTest" src="https://github.com/user-attachments/assets/ac9bd3f3-5fe2-462f-b00e-18034010249b" />

<img width="1919" height="1076" alt="LoggedFailedRDPAttempts" src="https://github.com/user-attachments/assets/d2f885df-5cf6-486a-9a0c-832ea2daf476" />

### Installing n8n (Automation Platform)

I could now move on to the second Ubuntu machine to install n8n, which would help organize the workflow and connects Splunk, OpenAI, and Slack together.

<img width="1780" height="950" alt="n8nInstalled" src="https://github.com/user-attachments/assets/3d672abf-e344-432b-8a28-3e57156ab750" />

### Connecting Splunk to n8n

After n8n was installed, I created a webhook in Splunk for the brute-force alert, so that it could be implemented into n8n's workflow.

<img width="1892" height="944" alt="WebhookSplunk n8n" src="https://github.com/user-attachments/assets/4b7563e4-ce64-4ed2-8a19-803ee39257c0" />

Test to ensure the webhook works correctly with the provided alert through n8n with 'Test-Brute-Force' alert from Splunk.

<img width="1818" height="934" alt="n8nTestOutput" src="https://github.com/user-attachments/assets/ef3f1621-31a4-4102-935e-a1d334cdee61" />

### Integrating OpenAI

To start automating the workflow, I added an 'OpenAI - Message a model' node in n8n and connected it to the webhook. This is also where the AI prompts can be created. 

In this case, I wanted a summary, any threat intelligence information based on the known threat, the severity of the attack, and recommended actions for the attack. This is also where I could add information for the AI to detect, such as the ComputerName, src_ip, user, and count.

<img width="1914" height="1071" alt="OpenAIPromptSetup" src="https://github.com/user-attachments/assets/2e839961-4069-4178-bdd5-46b84978f687" />

### Slack Integration

With the AI prompt ready, I moved to Slack to create a dedicated alerts channel that would output the AI responses. Then, I added a Slack node into n8n to send messages to the 'alerts' channel and executed the node with the message 'test' to ensure the response would be sent over to Slack.

<img width="1628" height="630" alt="SlackTest" src="https://github.com/user-attachments/assets/c7b6968c-11bd-4053-a990-cdaa304f954c" />

### Testing the Workflow

After confirming that n8n would send its response to Slack, I ran the workflow using the RDP failed logon attempts from earlier to see what the AI-generated response would be to the threat.

<img width="1915" height="968" alt="FirstAIResponseAttempt" src="https://github.com/user-attachments/assets/806a933a-5a8c-472c-9bbb-6f64e1908d20" />

### Adding Threat Intelligence

The responses were working correctly, however, because I was testing the attack through my host machine, it wouldn't give any threat intelligence, as the source IP was private.

To simulate a real-world scenario, I took out the original source IP (the private IP address used) and hardcoded a malicious source IP into the response from the site 'AbuseIPDB'. 

This was the malicious IP address that I used.

<img width="1915" height="1068" alt="ActualMaliciousIPUsed" src="https://github.com/user-attachments/assets/4bc27309-d449-4010-94ee-f9364809b798" />

I then added an AbuseIPDB node to the n8n workflow to automatically enrich the IP with reputation data.

Final Workflow:

<img width="1905" height="984" alt="FinalWorkflown8n" src="https://github.com/user-attachments/assets/11de0cf8-d8b8-44ac-9fe0-9857b5f651ba" />

### Final Output

After running the final workflow with the hardcoded malicious IP address, AI generated this response for this simulated brute force attack.

<img width="1897" height="867" alt="AIOutputMaliciousIP" src="https://github.com/user-attachments/assets/5285cf67-8609-4634-8905-c6ab973772ee" />












