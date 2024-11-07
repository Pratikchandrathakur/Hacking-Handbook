# Ethical Hacking Network Port Scanning Lab
This is an optional lab that you can do if you'd like to learn about how ethical hackers or penetration testers scan for open ports and services on a network or device.

## Introduction
What is an Ethical Hacker or Penetration Tester?
In cybersecurity, ethical hackers or penetration testers test the security of everything from computer networks, websites, and mobile applications to physical security. They perform testing by emulating or performing similar attacks and tactics that cybercriminals or threat actors use (a name we use in cybersecurity to describe a person or group who want to harm a digital device or system).

Often companies will contract penetration testers to perform testing on their network(s) to help identify any weaknesses so they can be fixed. In some cases, penetration tests are required yearly to meet compliance regulations.

## Performing Recon
In this lab, we'll be looking at one of the tasks performed by a network penetration tester. These testers specifically work to test the computer network of a business, in doing so they will look to compromise computers on the network and use their access to those computers to move to other computers inside the network.

One of the first steps a penetration tester will perform is recon on the network to identify what hosts (think computers) are present and also what services or ports they have open or are listening on. You may recall from the previous lesson on ports that an open port on a computer is an avenue for us to communicate with the underlying service or application that is listening on that port. The open ports represent what we call the attack surface for that computer as they are the different protocols or services that can be targeted over the network.

One popular tool to perform port and network scanning is nmap. In this lab we'll be learning how to use nmap to perform a port scan on a host.

## Proceed With Caution (Please Read This)
Before proceeding with the lab there are a few things to keep in mind.

In general scanning a computer or host that you don't have permission to is a bad idea. The legality of this can vary between regions with this being considered illegal in some regions. One of the golden rules of ethical hacking is only to test, scan, or hack thing that you own or have permission to.

In addition, nmap is a tool used by penetration testers and cybercriminals alike, using it on a school or company network may set off alarms from internal security tooling which could be investigated by the security team.

In this lab, we'll be scanning a target out on the internet that is hosted specifically for learning to perform scans. If you are going to go and use what you learned on another target please keep the above points in mind.

## The Lab
To follow along with this lab launch up your Ubuntu VM and open up the terminal.

Ubuntu doesn't come with nmap pre-installed so the first step will be to install it.
```
sudo apt install nmap
```
Once installed feel free to check out the man for nmap:
```
man nmap
```
Tip: to exit man press q.

Another great resource is to check out nmap's website and their examples:
```
https://nmap.org/book/man-examples.html

```
We're now ready to perform our first scan, to do so we'll target a host that the nmap org has set up for testing and gives permission to scan which is located at scanme.nmap.org.
```
nmap -v scanme.nmap.org

```
![image](https://github.com/user-attachments/assets/b48e532e-54ee-4787-b79e-b427f35371b9)

For me, at the time of scanning this, we can see there are 4 TCP ports open, 22 for ssh, 80 for HTTP, 9929 for nping-echo and 31337 the hacker number or in "LEET" speak Elite.

Nmap is capable of pulling down more details other than just the open port and the service, in fact, it can usually grab details about the actual application running and possibly even it's version.

Let's perform a more detailed scan with:
```
nmap -p- -A -T4 scanme.nmap.org
```
![image](https://github.com/user-attachments/assets/286e3dde-ded8-4332-819c-f7ccd2477454)

The -p option specifies the ports we want to scan, by passing in - to it, we are indicating we want to scan all TCP ports (65535 of them). The -A option enables aggressive scanning which attempts to detect operating system and application details. Finally -T is the speed at which the scan is performed with 1 being the slowest and 5 being the fastest. The faster the scan is performed the more likely it is to be detected by security tooling as the network will be flooded with traffic. In our example, we're not concerned with evading detection so we go with a speed of 4 (sometimes 5 is too fast and causes issues with the host or misses ports).



In my example at the time of scanning nmap was able to pull back versioning details for the SSH server running on the host. We can see it's using OpenSSH and the version. We also get details about the operating system of the computer as well.

These are all extremely valuable details for a penetration tester or attacker as we now know the software and version of one of the services listening on the open port. An attacker could perform further research to see if there are known exploits or vulnerabilities for this version of the software.

## Wrap-up
If you enjoyed this lab and learning about the ethical hacking process, make sure to check out the Practical Ethical Hacking course on the TCM Academy once you're finished this one!
