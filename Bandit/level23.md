Bandit Level 23 → Level 24
Today's Linux Lesson: Cron Jobs and Script Execution
What is a Scheduled Script Runner?
A scheduled script runner is a cron-launched program that executes other scripts or files automatically.

This can create a security risk when another user can influence files in a directory that a more privileged scheduled process later checks and executes.

The key is to understand the execution context: a file launched by a cron job runs with the privileges of the account executing that job.
Important Concepts
1. Cron can run scripts automatically under a designated account.
2. A script may iterate over files in a directory and decide which ones to execute.
3. Ownership checks can determine whether a file is eligible for execution.
4. A regular-file check (-f) verifies the file type, but does not by itself establish that execution is safe.
5. timeout limits how long a command runs; it does not change the command's privileges.
Most important takeaway: A directory used by a privileged scheduled script deserves careful scrutiny, especially if another user can influence its contents.
Investigating the Cron Job
Start by listing the cron definitions:
ls -la /etc/cron.d/
Then inspect the definition for the next account:
cat /etc/cron.d/cronjob_bandit24
The cron entry points to a script that runs periodically as bandit24.
Understanding the commands
Command / Argument	Description
ls -la /etc/cron.d/	Lists cron definitions, including permissions and ownership
cat	Displays the contents of a file
cronjob_bandit24	The cron definition associated with the next account


Inspecting the Scheduled Script
Read the script referenced by the cron entry:
cat /usr/bin/cronjob_bandit24.sh
The script changes into:
/var/spool/bandit24/foo
It then iterates over entries in that directory, checks their ownership, verifies that they are regular files, and executes qualifying files.

Important checks include:
stat --format "%U" "$i"
[ -f "$i" ]
Qualifying files are run using a command equivalent to:
timeout -s 9 60 "./$i"
Understanding the logic
1. stat --format "%U" "$i" obtains the owner of the current entry.
2. [ -f "$i" ] checks whether the entry is a regular file.
3. The script applies its ownership and file-type conditions before execution.
4. timeout -s 9 60 "./$i" runs the selected file with a time limit.
Examining the Directory
Inspect the directory's permissions, ownership, and contents:
ls -ld /var/spool/bandit24/foo
ls -la /var/spool/bandit24/foo
Compare what you find with the checks in the scheduled script.

The important question is not simply whether a file can be placed in the directory. You must also understand whether the cron script considers that file eligible for execution.
Why the execution context matters
The cron job runs as bandit24. A file that the job selects is therefore executed in that account's context, rather than automatically inheriting the privileges of the person who created it.

This is the security boundary worth understanding when reviewing scheduled script execution.
What Should You Investigate?
When examining a cron-based script runner, consider the following:
- Which account runs the cron job?
- Which directory does the script use?
- Who can write to that directory?
- How does the script check file ownership?
- Does it verify that entries are regular files?
- How are selected files executed?
- Is execution time limited?
- Could another user influence what the scheduled process executes?
Useful Commands
ls -la /etc/cron.d/
cat /etc/cron.d/cronjob_bandit24
cat /usr/bin/cronjob_bandit24.sh
ls -ld /var/spool/bandit24/foo
ls -la /var/spool/bandit24/foo
Key Takeaways
- Cron jobs execute with the privileges of their configured account.
- A scheduled script that executes files from a directory can create a privilege boundary.
- Ownership and file-type checks determine which entries are selected.
- A regular-file check alone does not make a writable execution directory safe.
- timeout limits execution duration, not execution privileges.
Lesson learned: When investigating scheduled execution, trace the cron definition, inspect the complete script, and pay close attention to directory permissions, ownership checks, and the account used to execute selected files.
