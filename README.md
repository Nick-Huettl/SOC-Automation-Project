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
- Integrate OpenAI to generate responses to simulated attacks.
- Send the AI-generated responses & alerts to Slack.

## Setup
