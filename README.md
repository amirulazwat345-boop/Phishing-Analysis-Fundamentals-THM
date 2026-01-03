# Phishing-Analysis-Fundamentals-THM

## Task 1: Introduction

Spam and phishing are both widespread social engineering attacks, but phishing through  email is especially dangerous. Spam has been around since the first unsolicited email in 1978 and continues to clutter inboxes today, often as a nuisance but sometimes carrying risks. Phishing, however, is more serious because attackers craft emails designed to trick users into clicking malicious links or downloading harmful attachments. Even with strong, layered defenses in place, a single unsuspecting employee can give attackers access to a corporate network.Email & Messaging

Security tools help reduce the number of malicious emails that reach users, but they are not perfect. This is why Security Analysts play a crucial role: they must investigate suspicious emails, determine whether they are malicious or benign, and gather intelligence to update defenses. By analyzing email headers and understanding how messages travel across the Internet, analysts can strengthen protections and prevent similar threats from reaching inboxes in the future. Practical exercises, such as dep.

**Questions:**

Read the task above

  | Answer: No answer needed

## Task 2: The Email Address

**Summary**

* Ray Tomlinson invented email in the 1970s on ARPANET and popularized the @ symbol
* An email address has:
  * User Mailbox (Username) - identifies the recipient
  * @ - separates the mailbox from the domain
  * Domain - guide where the message supposed to be sent to.
* Example: billy@johndoe.com
  * Mailbox: billy
  * @: separator
  * Domain: johndoe.com

**Questions**

Email dates back to what time frame?

  | Answer: 1970s

## Task 3: Email Delivery 

**Summary**

* SMTP: Handles sending emails from your client to mail servers.
* POP3: Downloads emails from the server to a single device.
* IMAP: Syncs emails across multiple devices by keeping them stored on the server.

**POP3 vs IMAP Differences**

* POP3
  * Emails are downloaded and stored locally
  * Sent messages stay only on the device you used.
  * Access is limited to that one device.
  * Unless "Keep email on server" is enabled, messages are deleted from the server after download
* IMAP
  * Emails remain on the server
  * Sent messages are stored on the server too
  * Messages can be accessed and synced across multiple devices

**How Emails Travel**

1. Compose: Alexa writes an email to Billy and hits send.
2. SMTP queries DNS: The sending server asks DNS where to deliver mail for johndoe.com..
3. DNS responds: DNS provides the destination mail server info.
4. SMTP sends: Alexa’s email is sent across the internet.
5. Relays: The email may pass through multiple SMTP servers.
6. Destination server: The email arrives at johndoe.com’s SMTP server.
7. Stored locally: The email is placed in Billy’s POP3/IMAP server mailbox.
8. Client checks: Billy’s email client queries the server for new mail.
9. Delivery: Email is downloaded (POP3) or synced (IMAP) to Billy’s device.

**Ports**

* SMTP: Default port 25 (others like 587 or 465 often used for secure sending).
* POP3: Default port 110 (995 for secure SSL/TLS).
* IMAP: Default port 143 (993 for secure SSL/TLS).

**Key Takeaway**

* SMTP = Sending
* POP3 = Download to one device
* IMAP = Sync across devices

**Questions**

What port is classified as Secure Transport (STARTTLS) for SMTP?

  | Answer: 587

What port is classified as Secure Transport for IMAP?

  | Answer: 993

What port is classified as Secure Transport for POP3?

  | Asnwer: 995

## Task 4: Email Headers

**Parts of an Email**

Every  email has two main components:

* Header: Metadata about the email (who sent it, when, through which servers).
* Body: The actual content (plain text or HTML).

Emails follow a standard syntax called the Internet Message Format (IMF).

**Key Header Fields**

When analyzing suspicious emails, start with the basics:

* From → Sender’s email address.
* Subject → Title of the email.
* Date → When the email was sent.
* To → Recipient’s email address.

**Raw Email Headers**

* X-Originating-IP → Shows the IP address where the email originated.
* SMTP.mailfrom / header.from → Domain the email was sent from (used in authentication checks).
* Reply-To → Address replies will go to (can differ from “From”).
  
👉 Example: An email might show From: newsletters@ant.anki-tech.com, but the Reply-To is reply@ant.anki-tech.com. This mismatch can be a red flag.

**Why Headers Matter**

* Attackers often spoof sender addresses to trick recipients.
* IP addresses and domains can help identify suspicious origins.
* Reply-To mismatches may indicate phishing attempts.

**Questions**

What email header is the same as "Reply-to"?

Answer can be found on: https://web.archive.org/web/20221219232959/https://mediatemple.net/community/products/all/204643950/understanding-an-email-header

  | Answer: Return-Path

Once you find the email sender’s IP address, where can you retrieve more information about the IP?

  | Answer: http://www.arin.net/.

## Task 5: Email Body

**Email Body Basics**

* The email body is the main content of the message.
* It can be plain text (simple words only) or HTML formatted (allows images, links, and styling).
* HTML makes emails more interactive but also introduces risks (hidden links, embedded code).

**Viewing HTML**

* Most  email clients let you switch between plain text and rendered HTML views.
* Example: In Protonmail, the option is called “View rendered HTML.”
* Each client (Yahoo, Gmail, Outlook, etc.) has slightly different steps.

**Attachments in Emails**

* Emails can include attachments (PDFs, images, etc.).
* Attachments are defined in the email’s source code with special
  headers:
    * Content-Type → File type (e.g., application/pdf, text/html).
    * Content-Disposition → Whether it’s an attachment or inline content.
    * Content-Transfer-Encoding → How the file is encoded (e.g., base64).
    * Networking
* Base64 data can be decoded to recover the actual file.

**Questions**

In the above screenshots, what is the URI of the blocked image?

<img width="768" height="432" alt="image-28-768x432" src="https://github.com/user-attachments/assets/9f66a6c4-0af3-4088-9ff8-d7e3e7da3114" />

  | Answer: https://i.imgur.com/LSWOtDI.png

In the screenshots above, what is the name of the PDF attachment?

<img width="581" height="259" alt="image-29" src="https://github.com/user-attachments/assets/8e0cf91f-a57f-4b38-a8ef-d4cbf3e3fa20" />

The name of the pdf file is in the top right.

  | Answer: Payment-updateid.pdf

In the attached virtual machine, view the information in email2.txt and reconstruct the PDF using the base64 data. What is the text within the PDF?

1. Start up machine on TryHackMe
2. open email2.txt file
3. copy based64 string
4. decode using Base64 with CyberChef: https://gchq.github.io/CyberChef/

<img width="1280" height="800" alt="Screenshot 2025-12-27 at 1 47 04 AM" src="https://github.com/user-attachments/assets/017789ef-13fd-45f9-b76a-375771323586" />

  | Answer: THM{BENIGN_PDF_ATTACHMENT}

## Task 6: Types of Phishing

**Types of Phishing & Malicious Emails**

* Spam → Bulk, unsolicited junk mail. Malicious variant = MalSpam.
* Phishing → Pretends to be a trusted entity to steal sensitive info.
* Spear Phishing → Targeted phishing aimed at specific individuals or organizations.
* Whaling → Phishing aimed at high‑level executives (CEO, CFO, etc.).
* Smishing → Phishing via SMS/text messages on mobile devices.
* Vishing → Phishing via voice calls.

**Objectives of Phishing**

* Harvest credentials (usernames, passwords).
* Gain access to victim’s  computer or network.

**Common Characteristics of Phishing Emails**

* Spoofed sender address (looks like a trusted entity).
* Urgent subject lines (e.g., “Invoice,” “Suspended”).
* HTML body mimics trusted brands (Amazon, Netflix, etc.).
* Poor formatting or grammar (contradicting the “professional” look).
* Generic greetings (“Dear Sir/Madam”).
* Hidden hyperlinks (often shortened to disguise origin).
* Malicious attachments disguised as legitimate documents.

**Safe Handling Practices**

* Never click suspicious links or attachments accidentally.
* Use defanging to make URLs/emails unclickable before sharing with SOC teams.
  * Example: http://www.suspiciousdomain.com → hxxp[://]www[.]suspiciousdomain[.]com.
* Tools like CyberChef can help automate defanging.

**Questions**

Analyze the email titled email3.eml within the virtual machine and answer the questions below.

Note: Alexa is the victim, and Billy is the analyst assigned to the case. Alexa forwarded the email to Billy for analysis. 

What trusted entity is this email masquerading as?

<img width="512" height="256" alt="Screenshot 2026-01-03 at 5 01 14 PM" src="https://github.com/user-attachments/assets/1b5992ae-aa49-4fa5-ba4d-e2fc0bb4389b" />

  | Answer: Home Depot

What is the sender’s email?

  | Answer: support@teckbe.com

What is the subject line? 

  | Answer: Order Placed : Your Order ID OD2321657089291 Placed Successfully

What is the website for the CLICK HERE URL in a defanged format? (e.g. https://website.thm)

<img width="1280" height="800" alt="Screenshot 2025-12-27 at 3 41 14 PM" src="https://github.com/user-attachments/assets/14732488-1a96-4213-9933-9cba85f17b26" />

  | Answer: hxxp[://]t[.]teckbe[.]com

## Task 7: Conclusion

A BEC is when an adversary gains control of an internal employee’s account and then uses the compromised email account to convince other internal employees to perform unauthorized or fraudulent actions. 

**Questions**

What is BEC?

  | Answer: Business Email Compromise

<img width="1280" height="800" alt="Screenshot 2025-12-27 at 3 41 37 PM" src="https://github.com/user-attachments/assets/b23cde97-c204-4f5c-8bc8-43f08186e0d6" />




