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











