# Inbound-Email-Containing-Suspicious-External-Link-3
This alert was triggered by an inbound email contains one or more external links due to potentially suspicious characteristics. As part of the investigation, check firewall or proxy logs to determine whether any endpoints have attempted to access the URLs in the email and whether those connections were allowed or blocked.
**Note:** The alert is generated from a relisble source (tryhackme).

**ALERT**
* datasource: email
* timestamp: 06/09/2026 11:59:39.541
*subject: Your Amazon Package Couldn’t Be Delivered – Action Required
* sender: urgents@amazon.biz
* recipient: h.harris@thetrydaily.thm
* attachment: None
* content: Dear Customer,\n\nWe were unable to deliver your package due to an incomplete address.\n\nPlease confirm your shipping information by clicking the link below:\n\nhttp://bit.ly/3sHkX3da12340\n\nIf we don’t hear from you within 48 hours, your package will be returned to sender.\n\nThank you,\n\nAmazon Delivery
* direction: inbound.

  STEP 1 I COMFIRMED THE ALERT IN IN SPLUNK. I RAN: <br>
  index=main h.harris@thetrydaily.thm
  <img width="740" height="235" alt="image" src="https://github.com/user-attachments/assets/d3febd4d-9be1-4ee0-a74a-d5422e36a031" />
This above event image comfirmed that the alert exist in splunk.

STEP 2 COMFIRM WETHER THE RECIPIENT CLICKED THE SUSPICIOUS LINK. I RAN: <br>
<img width="512" height="276" alt="image" src="https://github.com/user-attachments/assets/f5dd20aa-914c-4bb6-95d4-e3b100c86a5a" />
The above investigation event indicated that although the recipient clciked the suspiciousthe url link but was blocked by a firewall.

STEP3 COMFIRM HOW MANY HOST RECIEVED THE EMAIL: I RAN: 
<img width="960" height="247" alt="image" src="https://github.com/user-attachments/assets/dbd3cb7b-aeb6-4555-b3a0-a6a4cafd8e4d" />

The above event image indicated that only the recipient h.harris@thetrydaily.thm recieved the suspicious email with a phishing link.

**STEP 4 IOC:**
**Phishing Suspicious Email ioc** <BR>
* sender: urgents@amazon.biz
* recipient: h.harris@thetrydaily.thm
* subject: Your Amazon Package Couldn’t Be Delivered – Action Required

**URL Malicious IOC** <BR>
http://bit.ly/3sHkX3da12340 <BR>
Shorten URL for redirection to malicious/suspicious destination.

**Network External ioc** <br>
* Destination IP: 67.199.248.11

  **Internal Host IOC**
* Source IP (infected or targeted host):
10.20.2.17

  **CONCLUSION** <BR>
  This is a phishing attempt that was successfully blocked by a firewall. Though the email was recieved and the recipient attempted to click the suspicious link but firewall blocked it.

  **STEP 4 TRIAGE DECISION** <br>
* What happened?	A suspicious email that contained a phishing link was sent to a recipient. Recipient/user tried to access/click the Bitly link but was blocked by firewall rule <br>
* Is it real threat?	Unknown (suspicious indicator) <br>
* Impact?	Blocked by firewall, no compromise <br>
* Severity	medium <br>
* Result: monitor

  **Recommended Actions**
Verify ownership of 10.20.2.17 and confirm association with the recipient.
Scan the endpoint for malicious activity.
Block related IOCs across security controls.
Search for additional recipients of the same email.
Review proxy, DNS, and endpoint logs for further interaction attempts.
Notify the user and provide phishing awareness guidance.
