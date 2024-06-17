## Setting up passwordless access to the camera via SSH

Create a secret key on your desktop computer if it does not already exit.
Then use `ssh-copy-id` to upload the key to the target and establish secure authentication.

```
$ ssh-copy-id root@192.168.1.46
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/paul/.ssh/id_ecdsa.pub"
The authenticity of host '192.168.1.46 (192.168.1.46)' can't be established.
ED25519 key fingerprint is SHA256:PTcA1AMjGkoEHxa9EzVPamTdvYOSLkWKuHZZ6ilxZPw.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
root@192.168.1.46's password: 

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'root@192.168.1.46'"
and check to make sure that only the key(s) you wanted were added.
```

Then connect to the camera to verify the key-secured connection.

```
$ ssh root@192.168.1.46

  \\   _______ _     _ _____ __   _  ______ _____ __   _  _____
  )\\     |    |_____|   |   | \  | |  ____   |   | \  | |     |
 (  /     |    |     | __|__ |  \_| |_____| __|__ |  \_| |_____|
 / /
       t31n_gc2053_eth
       (HEAD+9310428, 2024-04-05 17:21:48 -0400

[root@thingino-t31n ~]# 
```

## Setting up passwordless SSH access from the camera to a remote host

### Generating an SSH key on the camera

By default, `droppear` generates a 256-byte ed25519 key.
You can change this using the `-t` parameter for key type (rsa, ecdsa, ed25519)
and `-s` for the key size, if necessary.

```
[root@thingino-t31l ~]# dropbearkey -f ~/.ssh/id_dropbear
Generating 256 bit ed25519 key, this may take a while...
Public key portion is:
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAICr3rGYlYj+SW5lfq1kRsrymriHbcYHYfmJHFmrKVrc5 root@thingino-t31l
Fingerprint: SHA256:6JuOtz9v5PDPofo3pBh/KQYgxJJMP2SVGy/Wuo8ba8I
```

### Adding the key to the remote system

Log in to the remote system and add the public part of your newly generated key to the `~/.ssh/authorized_keys` file.

```
echo "ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAICr3rGYlYj+SW5lfq1kRsrymriHbcYHYfmJHFmrKVrc5 root@thingino-t31l" | tee -a ~/.ssh/authorized_keys
```

### Testing access to the target using the key

Return to the camera shell and try to log in to the target system using the key.

```
[root@thingino-t31l ~]# ssh paul@192.168.1.61

Host '192.168.1.61' is not in the trusted hosts file.
(ssh-ed25519 fingerprint SHA256:6mlqFLKOO5FXQpN5H2pGJZgcPj3mSO3J0rr79T82hQ8)
Do you want to continue connecting? (y/n) y
Linux owlnest 6.7.9-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.7.9-2 (2024-03-13) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.

21:35:02/@107 paul@owlnest:~
$ 
```
