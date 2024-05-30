# Data402_SSH_Test
Sparta Week 6 Day 3 SSH (Bank Holiday Week)

# Shells and Ports

A **shell**: an interface where you can communicate with a piece of software, it exposes an operating system's services to a human user or other programs. <br><br>
A **port**: a point of connection, where that connection will start and end. They are managed by a machine's operating system, think of it like the dentist's receptionist (OS) telling you which room (port details) to see the dentist in (the software)<br><br>
James O'Brien: *"I like to use the metaphor of a large docksite. A docksite has ports for ships, but before they can be put there they need permission, an open port, so the ship would send a notification to say they want to port there, and the response would have to be an open port to allow them to come in. What you don't want is to open all of the ports whenever, as just like with these ships you wouldn't know what is coming in otherwise."*

Github is a remote set of servers, one holds your repo. You can use an SSH key to verify who you are from your local machine.

There is an SSH public key and a private key. The private key is the key to your server, it connects to your public key, and it should be held locally. The public key is less strict on who sees it, it's like the lock on your front door. Look at the diagram for Week 6 SSH security.

# SSH Key Steps

### WHEN YOU ARE GENERATING AN SSH KEY TO CONNECT A REPO TO YOUR LOCAL MACHINE:

In Git Bash: <br>
run "cd" to go to base directory <br>
then run "cd .ssh" to go to hidden ssh files

Run:
ssh-keygen -t rsa -b 4096 -C "sammy.smith@outlook.com"

*Breakdown of above function*:<br>
ssh-keygen: asking the system to generate a key pair<br>
-t: indicates the type of ssh key<br>
rsa: very popular type of ssh key<br>
-b: stands for "bits", how long will the encrypted string be?<br>
4096: length of the string<br>
-C: comments attached with the command<br>
"<\email>": adding the email of who has created the pair<br>

Use the following to display your public key:<br>
sudo nano git_test_key.pub
OR
cat git_test_key.pub

This should print the public key in your shell, right click and copy without any whitespace

Now, go to your repo on Github, and go to Settings and 'Deploy keys'.<br>
Add your Title (preferably with _key on the end)<br>
Paste the ssh key and REMEMBER TO TICK 'ALLOW WRITE ACCESS'

***NEVER*** WRITE GIT COMMANDS IN YOUR .SSH FOLDER!

### IF YOU ARE CLONING USING AN SSH KEY
In another Git Bash window:
run "eval `ssh-agent`" in the file you stored your repo in

run `ssh-add ~/.ssh/git_test_key<br>
Output: Identity added: '\<file directory>\<email>'

run `ssh -T git@github.com`<br>
Output: Hi SamDavidSmith/\<repo>! You've successfully authenticated, but GitHub does not provide shell access.

Now, you can clone with git clone <ssh-link> shown on Github in the directory.

You will be able to push/pull in this second Bash window ***as long as*** it is kept open!
