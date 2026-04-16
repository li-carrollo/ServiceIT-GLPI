# ServiceIT-GLPI
this is a glpi instance 

Supports ticket submission via email, web portal, and phone/manual entry

Connect Email Receiver:
Path: Setup > Receivers
Protocol: Use IMAP (over SSL/TLS) for reliability.
Note: Configuration details must be adapted from the personal Gmail test to the official afp.mil.ph domain.
Connection String: {imap.gmail.com:993/imap/ssl/novalidate-cert}INBOX
Automate Email Fetching (Mailgate Cron Job):
In GLPI: Go to Setup > Automatic actions > mailgate.
Run Mode: Change to CLI (Command Line Interface).
Run Frequency: Set to 1 minute or 5 minutes.
System Setup (Crontab):
Step 1: Locate the GLPI background task engine file (front/cron.php) on your server.
Verified Path Example: /var/www/glpi_source/front/cron.php
Step 2: Open the crontab editor with sudo crontab -u www-data -e.
Step 3: Add the automation line to run the job every minute (replace [YOUR_PATH] with the path from Step 1):
*/1 * * * * /usr/bin/php [YOUR_PATH]
B. Web Portal (Self-Service)

This allows end-users to submit tickets through a web interface.
Configuration: Create a user in Administration > Users and assign them the Self-Service profile.
Verification: Log in as that user to confirm the "Simplified Interface" is active. No extra plugins are required.
C. Outgoing Notifications (Email Replies)

This ensures users receive confirmation emails when a ticket is submitted or updated.
C.1 SMTP Setup:
Path: Setup > Notifications > Email Notifications Configuration.
Set Way of sending email to SMTP
Set Check Certificate to No
Host/Port: smtp.gmail.com | port: 465.
Authentication:  Use the personal  email and 16-character App Password.
Send a test email to the administrator to verify 
C.2 Triggering the Notification:
Enable: Set "Enable notifications" to Yes in Setup > Notifications.
Self-Notification: Set "Notifications for my own changes" to Yes.
Automation: In Setup > Automatic actions, find queuednotification and change its Run Mode to CLI to ensure emails are sent regularly.
D. Manual / Phone Entry

This allows technicians to manually create a ticket.
Path: Assistance > Tickets > [+] Add.
Verification: Ensure technicians can select "Phone" or "Direct Request" from the Source of Request dropdown.



