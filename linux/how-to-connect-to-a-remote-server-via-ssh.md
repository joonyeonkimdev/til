# How to Connect to a Remote Server via SSH
> SSH(Secure Shell) is a cryptographic protocol that allows you to securely connect to a remote server.  
> An SSH Connection having been established, a session started for a shell where you can manipulate the remote server by commands.
>  
> Steps for an SSH Connection
> 1. Generate SSH Keys in the Client Host
> 2. Copy the Public Key in the Client into the Remote Server
> 3. Connect

## 1. Generate SSH Keys in the Client Host
```shell
ssh-keygen -t rsa
```
Create SSH key by running the command. It consists of a public and private key.  
You can determine the algorithm with the option `-t`.  

When you run this command, you come to face the following setting line for the path for the keys. 
The default path of the keys, when you enter nothing, is `~/.ssh`.  
After the path setting, `passphrase` setting follows and 
if you'd like SSH connections to do with automatic log-in, you must enter nothing in this setting. 

## 2. Copy the Public Key in the Client into the Remote Server
After the keygen command, you can find the private key file `id_rsa` and the public `id_rsa.pub` in the directory you set.  
Copy the whole contents in the 'id_rsa.pub' file in the client server into the file `authorized_keys` in the directory `~/.ssh` in the remote server.  
Keep in mind that you do not replace the contents in the 'authorized_keys' file but add the public key to 
because the file may have other public keys for other servers.

## 3. Connect
```shell
ssh [username]@[host_ip_address]
```
