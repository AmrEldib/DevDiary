# Problem

How to SSH into Synology as Root?

# Solution

I posted this as an answer on [Superuser](http://superuser.com/a/1168644/96992)  

> SSH/Telnet only supports logging into the system with accounts belonging to the administrators group. To switch to a root account, please log into the system with SSH/Telnet as a user belonging to the administrators group, run the command sudo -i, and then enter the password of the account used to log in.  

```bash
sudo -i
```

[Source](https://www.synology.com/en-us/knowledgebase/DSM/tutorial/General/How_to_login_to_DSM_with_root_permission_via_SSH_Telnet)

# Problem 

How to SSH to custom port

# Solution

```bash
ssh -p 23 admin@machine
```