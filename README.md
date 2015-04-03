SSHPASS-P4K
===========

sshpass-p4k is modified version of sshpass for handling also ssh key authentication with passphrases,
 e.g. when ssh client prompts passphrase for key. Passphrase is supplied like password to sshpass via
 command line parameters (-p), environment variable (-e), line from file (-f) or file descriptor (-d).
 See [sshpass man page](http://linux.die.net/man/1/sshpass) for more details.

P4K suffix is abbreviation from passphrase-for-key = pass4key = P4K

There are no other modifications to sshpass except providing passphrase on ssh prompt "passphrase for key".

SSH-AGENT
=========
ssh-agent offers the same functionality, but the passphrase has to be entered in advance so decrypted
 private key could be kept in memory. Therefore on logout, reboot etc the decrypted memory key is lost
 and has to be again entered interactively by the user.

See [ssh-agent man page](http://linux.die.net/man/1/ssh-agent) for more details.

Pros
====
The main motivation behind sshpass-p4k is ability to execute non-interactive ssh key authenticated
 batch/cron jobs in QA environment for automation testing. Ssh-agent due to security concerns should
 not be used in production environment (use ssh-agent), please se cons bellow.

Cons
====
There are security implications from storing password or/and passphrase on the system, see 
 [sshpass man page](http://linux.die.net/man/1/sshpass) for more details. Never store passwords or passphrases
 on production systems. You have been warned.

When to use sshpass-p4k
=======================
Cron jobs, batch jobs which cannot for whatever reason use ssh-agent would benefit from sshpass-p4k.
 If you don't need key based authentication with passphrases stay with original sshpass, you will not
 benefit from using sshpass-p4k. However, even in this case by using sshpass-p4k you will not loose
 anything and you can easily switch to hey based authentication in the future.

no key based authentication -> stay with sshpass

key based authentication -> consider ssh-agent, if cannot -> use sshpass-p4k

Hope this helps,
Robert