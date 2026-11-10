# H3 - Cyber lab

In this lab excercise I will install Linux Debian 13 Trixie into virtual machine and test some commands and tools, especially Hashcat for cracking passwords.

## Read and summarize

Before starting I will read and summarize articles about topics below.

### How to install Linux to Virtualbox

The article discussed the installation of VirtualBox on Windows 11, the downloading of a Debian ISO image, and provided a more detailed explanation of creating a virtual machine in VirtualBox and installing Debian Linux into VM.

* First thing is to check that VT-X is enabled in the host machine UEFI/BIOS
* Download the latest suitable Linux ISO image
* Virtualbox setting 'Proceed with Unattended Installation' enabled may cause installation to fail
* Install Debian by starting 'Install Debian' from desktop when Debian Live from ISO -file is up and running
* Remember to run updates on your freshly installed system

* In my AMD based system BIOS setting for virtualization is AMD V(TM) Technology
* If Debian Live session gets locked due inactivity the required credentials are user / live

Installing Debian using installer found on Debian live desktop is quite straight forward. Partitioning the disk could be the trickiest part, but the default selections work well in this case. 

### Command line basics

The article goes trough some basic commands used in Linux terminal or shell. Some of the commands are same than ones used in Windows command prompt or powershell.

* Essential commands to memorize are listing, creating, moving, deleting and editing files and directories
* Learn how to use text editor such nano, pico or vi
* Use sudo command to run other commands with higher privileges, but only when necessery


### Cracking password with Hashcat



## Installing Linux on a virtual machine

I already had two virtualization software options available for hosting the virtual machine. First one was Hyper-V running on Windows 11 OS and second one was Proxmox Virtual Environment. Proxmox is open-source and more bare-metal type hypervisor that is build on custom Debian Linux. I decided to go with Proxmox for more customization options.

I did Google search with keywords "proxmox vm settings for debian 13" to get any Proxmox specific recommendations for VM hardware or settings. Search AI Overview recommended machine type q35 meaning never virtual hardware which is fine. There was no recommendation about graphic card so I chose default.

### VM settings for Debian 13

I created new virtual machine using settings below.

* Guest OS: Linux (v7.x - 2.6 Kernel)
* Machine: q35
* BIOS: OVMF (UEFI)
* QEMU Guest Agent: Enabled

* CPU: sockets 1, cores 4
* Graphics card: default
* Memory: 4096 MB
* Disk: 40 GB
* Network: VirtIO (paravirtualized)

### Installing Debian

When installing any OS on Proxmox virtual environment you need to upload ISO-image to Proxmox ISO-repository first. ISO-image can be uploaded using Proxmox GUI.

![ISO-image upload](img/h3/h3-01-upload.PNG)

Update Debian packages and install Qemu-guest-agent. Qemu Guest Agent is used to exchange information between the Proxmox host machine and VM, and also to execute command in the VM OS. 

```
sudo apt update
sudo apt full-upgrade
sudo apt install qemu-guest-agent 
```

Until this point I had used Proxmox noVNC console for operating in VM, and I noticed that clipboard is not working between VM and management workstation. It would be anyways more convinient to remote connect using SSH, so I decided not test any workarounds on noVNC. Let's install SSH server.  

```
sudo apt install ssh
```


## Cracking password with Hashcat

The goal was to crack password with hash 6b1628b016dff46e6fa35684be6acc96. I used instructions from Tero's article discussed earlier 'Cracking passwords with Hashcat'

I started by installing tools required Hashcat and wget for downloading password dictionary called Rockyou.

```
sudo apt install hashid hashcat wget
```

Downloading Rockyou dictionary, unpacking tar -archive and finally deleting compressed tar.gz archive.

```
wget https://github.com/danielmiessler/SecLists/raw/master/Passwords/Leaked-Databases/rockyou.txt.tar.gz
tar xf rockyou.txt.tar.gz
rm rockyou.txt.tar.gz
```

Count lines command reported 14 344 391 password in the file.

```
wc -l rockyou.txt
14344391 rockyou.txt
```


```
hashid -m 6b1628b016dff46e6fa35684be6acc96

Analyzing '6b1628b016dff46e6fa35684be6acc96'
[+] MD2
[+] MD5 [Hashcat Mode: 0]
[+] MD4 [Hashcat Mode: 900]
[+] Double MD5 [Hashcat Mode: 2600]

```
There are few options for hash type, but in this case MD5 is more likely right one.

```
hashcat -m 0 '6b1628b016dff46e6fa35684be6acc96' rockyou.txt -o solved
```
Hashcat output while running: 

```
hashcat (v6.2.6) starting

OpenCL API (OpenCL 3.0 PoCL 6.0+debian  Linux, None+Asserts, RELOC, SPIR-V, LLVM 18.1.8, SLEEF, DISTRO, POCL_DEBUG) - Platform #1 [The pocl project]
====================================================================================================================================================
* Device #1: cpu-penryn-QEMU Virtual CPU version 2.5+, 1413/2890 MB (512 MB allocatable), 4MCU

Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 256

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Rules: 1

Optimizers applied:
* Zero-Byte
* Early-Skip
* Not-Salted
* Not-Iterated
* Single-Hash
* Single-Salt
* Raw-Hash

ATTENTION! Pure (unoptimized) backend kernels selected.
Pure kernels can crack longer passwords, but drastically reduce performance.
If you want to switch to optimized kernels, append -O to your commandline.
See the above message to find out about the exact limits.

Watchdog: Hardware monitoring interface not found on your system.
Watchdog: Temperature abort trigger disabled.

Host memory required for this attack: 0 MB

Dictionary cache built:
* Filename..: rockyou.txt
* Passwords.: 14344391
* Bytes.....: 139921497
* Keyspace..: 14344384
* Runtime...: 1 sec


Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 0 (MD5)
Hash.Target......: 6b1628b016dff46e6fa35684be6acc96
Time.Started.....: Tue Nov 10 08:28:15 2026 (0 secs)
Time.Estimated...: Tue Nov 10 08:28:15 2026 (0 secs)
Kernel.Feature...: Pure Kernel
Guess.Base.......: File (rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:    17101 H/s (0.10ms) @ Accel:256 Loops:1 Thr:1 Vec:4
Recovered........: 1/1 (100.00%) Digests (total), 1/1 (100.00%) Digests (new)
Progress.........: 1024/14344384 (0.01%)
Rejected.........: 0/1024 (0.00%)
Restore.Point....: 0/14344384 (0.00%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidate.Engine.: Device Generator
Candidates.#1....: 123456 -> bethany

Started: Tue Nov 10 08:27:47 2026
Stopped: Tue Nov 10 08:28:16 2026

```
Cracking succeeded and after dictionary cache build took less than a second.

Final result in file 'solved' contained hash and cracked password.

```
cat solved
6b1628b016dff46e6fa35684be6acc96:summer
```

I did another run with new MD5 hash and slightly longer, but still weak password. New hash is generated using md5sum command.

```
printf '%s' "summer123" | md5sum
070af46980fb7b42bdaa8bb48460dfff  -

hashcat --potfile-disable -m 0 '070af46980fb7b42bdaa8bb48460dfff' rockyou.txt -o solved2

cat solved2
070af46980fb7b42bdaa8bb48460dfff:summer123
```

This time as well, finding the correct password took less than a second.

## Conclusion

This example clearly illustrates why strong passwords are important. Even a slightly longer password can be cracked very quickly if it consists only of a dictionary word and numbers. 
