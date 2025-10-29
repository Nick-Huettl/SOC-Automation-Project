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

## Setup

The initial setup included downloading VMware Workstation and creating the virtual machines that would be needed for the project. I started with the Windows 11 machine, as this will be the machine that sends its telemetry and logs over to Splunk.

<img width="1919" height="1075" alt="VMsetupComplete" src="https://github.com/user-attachments/assets/ca6c1309-6d02-49bf-9391-120e30aab775" />

After the Windows 11 machine was downloaded and running, I created a snapshot in case anything were to happen, so that the base Windows 11 machine could be restored if needed. I then moved on to the Ubuntu server that would host Splunk. This was done by using the command line on Ubuntu and using the wget link provided on Splunk's site after creating an account.

Once installed, I could go over to my host machine's browser and enter the Ubuntu VM's IP address and the port number 8000 (Splunk's default web interface port number) to reach the Splunk interface and sign in with the credentials I created.

<img width="1640" height="938" alt="SplunkInstalledUbuntu" src="https://github.com/user-attachments/assets/f2ee9743-ac68-403d-aef4-57541504d287" />

With Splunk up, there were a few things that needed to be configured, such as creating a new index that would eventually display the Windows 11 telemetry and logs.

However, I needed to connect the Windows 11 VM and the Splunk instance, so I went back to the Splunk website and got the install for the Splunk forwarder. This would allow the information to be sent over to Splunk once configured properly. 

<img width="1915" height="974" alt="VMForwardingTelemetrySplunk" src="https://github.com/user-attachments/assets/bf5fb0ae-7552-4019-92db-8e1cf5b0c1d5" />

Now that Splunk is receiving the telemetry and logs, I could test to ensure that Splunk would receive the brute force attack attempt. This was done by simply trying to RDP into the Windows 11 machine unsuccessfully with the wrong password. This can then be found using the 'EventCode=4625' query to narrow the logs down to unsuccessful Window logon attempts.

<img width="1713" height="903" alt="FailedAttemptsRDPTest" src="https://github.com/user-attachments/assets/ac9bd3f3-5fe2-462f-b00e-18034010249b" />

<img width="1919" height="1076" alt="LoggedFailedRDPAttempts" src="https://github.com/user-attachments/assets/d2f885df-5cf6-486a-9a0c-832ea2daf476" />








