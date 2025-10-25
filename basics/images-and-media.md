---
icon: book-blank
---

# Logs

#### Field Definitions for Beelzebub Logs

Here is the structured JSON definition of each field in Beelzebub logs:

* Command: The command entered by the attacker.
* CommandOutput: The honeypot's response.
* DateTime: The date and time of the attack.
* Description: A description of the honeypot configuration.
* ID: The unique identifier for each attack.
* Location: Details regarding the attack's origin.
* Msg: Information regarding the state callback.
* Protocol: The protocol used by the honeypot (SSH, HTTP, or TCP).
* RemoteAddr: The attacker's IP address and local post (IP:Port).
* Status: The interaction stage (Start, Stop, or Interaction). In an SSH session, the status is Interaction.
