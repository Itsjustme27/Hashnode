---
title: "Emotet pcap analysis"
seoTitle: "Emotet Network Traffic Dissection"
seoDescription: "Analyze Emotet malware in a pcap file using Wireshark, uncovering details like IP address, hostname, and infection timeline"
datePublished: Sun Nov 02 2025 17:05:06 GMT+0000 (Coordinated Universal Time)
cuid: cmhhyoywl000102l14kqidysa
slug: emotet-pcap-analysis
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1762103096958/31edeffd-ac22-4e74-87cf-c0a6bc36b0d9.png
tags: networking, cybersecurity, forensics, emotet, wireshark

---

### TL ; DR

Even though i mostly looked at the solved writeups, I solved half of it myself unknowingly lol.

### Background

Today, i got curious on how to actually apply the things i learnt in Wireshark, so i searched up some platforms and found a pcap file from [ISC Diary - December 2021 Contest: Forensic Challenge](https://isc.sans.edu/diary/December+2021+Forensic+Challenge/28108) and went in blind.

### Challenges

Provide the following information:

* IP address of the infected Windows computer.
    
* Host name of the infected Windows computer.
    
* User account names from the infected Windows computer.
    
* Date and time the infection activity began in UTC (the GMT or Zulu timezone).
    
* The family of malware that caused this infection.
    

### Answers

* Infected IP: `10.12.3.66`
    
* Hostname: `DESKTOP-LUOABV1`
    
* User: `darin.figueroa`
    
* Start: `2021-12-03 19:42:47 UTC`
    
* Family: `Emotet`
    

## Analysis

After trying things on my own and unintentionally solving half the challenges, here are the steps and wireshark filters i took:

```plaintext
nbns
```

![](https://isc.sans.edu/diaryimages/images/2021-12-22-ISC-diary-image-02a.jpg align="left")

I found that there is only one Windows client, which was suspicious.

Then i tried the kerberos filter since it was under the Active Directory(AD).

```plaintext
kerberos.CNameString
```

The `CNameString` outputs the AD username.

![](https://isc.sans.edu/diaryimages/images/2021-12-22-ISC-diary-image-03a.jpg.jpg align="left")

As you can see, *the Windows user account name through Kerberos traffic* `darin.figueroa`

Now, this is where i got stuck, i didn’t know where to look after this, so i looked up in the writeup/solution, and found out a simple HTTP filter can sort things out.

```plaintext
(http.request or tls.handshake.type eq 1) and !(ssdp)
```

What this basically does is, tells wireshark to "Show me any unencrypted HTTP request packet **OR** any initial HTTPS Client Hello packet, **BUT** make sure none of them are SSDP packets."

![](https://isc.sans.edu/diaryimages/images/2021-12-22-ISC-diary-image-01a.jpg align="left")

The two HTTP URLs used to retrieve the Emotet DLL were:

* ***hxxp://gamaes\[.\]shop/wp-content/plugins/sSTToaEwCG5VASw/***
    
* ***hxxp://newsaarctech\[.\]com/wp-content/Sx9tvV5/***
    

Then i got curious and went over to VirusTotal to check these links, and conveniently, they were actual live malwares.

The following IP addresses over TCP port 443 have been reported as C2 channels for Emotet:

* 172.104.227.98 port 443   *\[*[*Link*](https://feodotracker.abuse.ch/browse.php?search=172.104.227.98) [*to*](https://feodotracker.abuse.ch/browse.php?search=163.172.50.82) *IP address in Feodo Tracker\]*
    
* 163.172.50.82 port 443   *\[*[*Link*](https://feodotracker.abuse.ch/browse.php?search=163.172.50.82) *to IP address in Feodo Trac*[*ker\]*](https://feodotracker.abuse.ch/browse.php?search=163.172.50.82)
    

With a basic web filter, scroll down a bit to find SSL/TLS [traf](https://feodotracker.abuse.ch/browse.php?search=163.172.50.82)fic using TCP ports 465 and 587 starting at 20:09 UTC.  This r[epre](https://feodotracker.abuse.ch/browse.php?search=163.172.50.82)sents encrypted SMTP traffic, and it reveals our Emotet-infected host also acted as a spambot.  Emotet uses Emotet-infected Windows hosts to help distribute new Emotet malspam.

![](https://isc.sans.edu/diaryimages/images/2021-12-22-ISC-diary-image-04a.jpg align="left")

Then, once again, i got stuck, oof, and looked it up at the solution and found out that since Emotet just spams mail on hosts, why not check the `SMTP`??

Yep, Thats what i did (shamefully copying)

![](https://isc.sans.edu/diaryimages/images/2021-12-22-ISC-diary-image-05a.jpg align="left")

Since we cant really read raw data properly, we will be using

```plaintext
smtp.data.fragment
```

![](https://isc.sans.edu/diaryimages/images/2021-12-22-ISC-diary-image-06a.jpg align="left")

You can extract these 17 emails using ***File --&gt; Export Objects --&gt; IMF...*** as shown below.

![](https://isc.sans.edu/diaryimages/images/2021-12-22-ISC-diary-image-07a.jpg align="left")

All of these emails are spoofed replies to legitimate email chains collected from previously-infected Windows hosts.  All of these emails have attachments.  Some of the attachments are Excel spreadsheets.  Other attachments are password-protected zip archives.  We can review the emails using an email client. Well, Linux automatically opens ThunderBird or something, so i will go with that.

![](https://isc.sans.edu/diaryimages/images/2021-12-22-ISC-diary-image-08a.jpg align="left")

**Attachment : Excel spreadsheet**

And that’s how i successfully managed to solve the forensics challenge.

**Images and original solutions/writeups source:**

```plaintext
https://isc.sans.edu/diary/December+2021+Forensic+Contest+Answers+and+Analysis/28160
```