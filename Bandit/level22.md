Bandit Level 22 → Level 23
Today's Linux Lesson: Cron Jobs and Predictable Filenames
What is a Cron Job?
Cron is a Linux service used to schedule commands or scripts to run automatically at specified times or intervals.

A cron job runs under the privileges of the user configured to execute it. This matters during security investigations because a scheduled task may access files or perform actions that the current user cannot perform directly.
Important Concepts
1. Cron jobs execute commands automatically according to a schedule.
2. The user associated with a cron job determines the privileges used to run it.
3. Cron definitions commonly live in locations such as /etc/cron.d/.
4. Scripts called by cron should be inspected to understand what they do and which files they access.
5. A predictable filename generated from known input can often be reproduced.
Most important takeaway: Always investigate both the cron definition and the script it launches. The cron entry tells you when and as whom something runs; the script tells you what actually happens.
Investigating the Cron Job
First, list the cron definitions:
ls -la /etc/cron.d/
Then inspect the job for the next account:
cat /etc/cron.d/cronjob_bandit23
The entry points to a script that runs periodically as bandit23.
Understanding the command
Command / Argument	Description
ls -la /etc/cron.d/	Lists cron definitions, including permissions and ownership
cat	Displays the contents of a file
cronjob_bandit23	The cron definition associated with the next account


Inspecting the Scheduled Script
Read the script referenced by the cron entry:
cat /usr/bin/cronjob_bandit23.sh
The important logic is:
myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)
cat /etc/bandit_pass/$myname > /tmp/$mytarget
Understanding the logic
1. whoami identifies the user running the script.
2. The script builds the string I am user <username>.
3. md5sum calculates an MD5 hash of that string.
4. cut extracts the hash value from the command output.
5. The password file for the running account is copied to /tmp/ using that hash as the filename.
Because the input string is predictable, the resulting filename can be calculated.
Reproducing the Filename
The cron job runs as bandit23, so reproduce the same input:
echo I am user bandit23 | md5sum
Use the resulting hash to inspect the corresponding file:
ls -l /tmp/<hash>
If the file is readable, display its contents:
cat /tmp/<hash>
The file contains the credential needed for the next level. The password is intentionally omitted from this public write-up.
What Should You Investigate?
When examining cron jobs, consider the following:
- Which user executes the job?
- How often does it run?
- Which script or command does it execute?
- Does the script read or write sensitive files?
- Does it create temporary files?
- Are filenames or paths predictable?
- What permissions apply to the generated files?
Useful Commands
ls -la /etc/cron.d/
cat /etc/cron.d/cronjob_bandit23
cat /usr/bin/cronjob_bandit23.sh
whoami
Key Takeaways
- Cron jobs are scheduled tasks that run under a specific user's privileges.
- The cron definition and the script it calls must both be inspected.
- MD5 hashes can be reproduced when the input is known; they do not make predictable data secret.
- Temporary files can reveal useful information, but their permissions still control access.
Lesson learned: Follow the execution chain, identify the account running the job, and understand how the script generates and uses filenames.
