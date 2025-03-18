Script
[olphnt / olitools / ecol_controllers / ecol_sendmail.py — Bitbucket](https://bitbucket.org/olphnt/olitools/src/master/ecol_controllers/ecol_sendmail.py)

The Script looks in the SMB Mounted Folder /automation/EMAIL/INPUT [[How to mount a CIFS share to a container in Docker Desktop]] for Emails to render and send, If it finds the custom domain field in those csv files containing the email data then it changes the sender domain in the Mailgun api.