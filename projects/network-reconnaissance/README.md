# Network Reconnaissance Lab

## Objective

Practice authorized host and service discovery with Nmap, then translate observed exposure into defensive recommendations.

## Environment and scope

- Scanner: Kali Linux in Oracle VirtualBox
- Target: Metasploitable 2, an intentionally vulnerable Linux VM
- Network: VirtualBox host-only network
- Target address: `192.168.56.102`
- Scan command: `nmap -sV -oN metasploitable-scan.txt 192.168.56.102`
- Scope: one lab target, TCP services identified by Nmap service/version detection

## Observed services

Nmap reported 23 open TCP ports and 977 closed TCP ports in its default scan range.

| Port(s) | Nmap service/version observation |
|---|---|
| 21 | FTP, vsftpd 2.3.4 |
| 22 | SSH, OpenSSH 4.7p1 Debian 8ubuntu1 |
| 23 | Telnet, Linux telnetd |
| 25 | SMTP, Postfix smtpd |
| 53 | DNS, ISC BIND 9.4.2 |
| 80 | HTTP, Apache httpd 2.2.8 (Ubuntu), DAV/2 |
| 111 | rpcbind 2 |
| 139, 445 | NetBIOS/SMB, Samba smbd 3.X–4.X |
| 512 | rexecd, netkit-rsh |
| 513 | rlogin, OpenBSD or Solaris rlogind identification |
| 514 | shell, Netkit rshd |
| 1099 | Java RMI, GNU Classpath grmiregistry |
| 1524 | Bind shell, Metasploitable root shell label |
| 2049 | NFS 2–4 |
| 2121 | FTP, ProFTPD 1.3.1 |
| 3306 | MySQL 5.0.51a-3ubuntu5 |
| 5432 | PostgreSQL 8.3.0–8.3.7 |
| 5900 | VNC protocol 3.3 |
| 6000 | X11 (access denied) |
| 6667 | IRC, UnrealIRCd |
| 8009 | AJP/1.3 |
| 8180 | HTTP, Apache Tomcat/Coyote JSP engine 1.1 |

## Defensive recommendations

- Remove services that are not required; prioritize Telnet, legacy `rexec`/`rlogin`/`rsh`, and the bind-shell listener.
- Use encrypted administrative protocols, restrict SSH access, and keep supported software patched.
- Restrict database, SMB, NFS/RPC, RMI, AJP, VNC, X11, and other service access to necessary trusted systems.
- Review web applications and server configuration, remove unused components, and use HTTPS where sensitive data is handled.
- Re-scan after changes to confirm exposure has been reduced.

## Limitations

This was a service/version scan of one deliberately vulnerable training VM. Nmap's version strings are identification hints, not proof that a vulnerability is exploitable. The command scanned the default TCP port range; UDP services and authenticated configuration were not assessed.

## Reproduction

With the authorized target running on the isolated lab network:

```bash
nmap -sV -oN metasploitable-scan.txt 192.168.56.102
```

The raw output was saved as `metasploitable-scan.txt` in Kali and is not bundled in this repository because the capture/output file was not transferred from the VM.