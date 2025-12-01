---
title: "Advent of Cyber Prep Track THM"
seoTitle: "Prepare for Advent of Cyber THM"
seoDescription: "Prepare for Advent of Cyber 2025 with interactive cybersecurity challenges and master essential skills to help save SOCMAS in Wareville"
datePublished: Mon Dec 01 2025 15:00:30 GMT+0000 (Coordinated Universal Time)
cuid: cmina0f7u000602ld0odke0mh
slug: advent-of-cyber-prep-track-thm
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1764601364437/04ea416d-e412-41b4-babb-fe803fdd9f34.jpeg
tags: cybersecurity, tryhackme, adventofcyber2025

---

## 1\. Introduction

### Let's Get Warmed Up

The snow has started falling in **Wareville**, home of *The Best Festival Company (TBFC)*. The team is preparing for SOCMAS, the annual cyber celebration, but something’s not right. Systems are glitching, passwords are failing, and McSkidy suspects something is afoot. This name keeps coming up: **King Malhare**. What could it mean?

Before joining the **SOCMAS Response Team**, you can complete **10 short missions** to ensure you are ready. Each one teaches an essential cyber security skill and uncovers clues to help get you ready for Advent of Cyber 2025.

![McSkidy warming her hands by a fire](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/6228f0d4ca8e57005149c3e3-1763127196624.png align="left")

## How it Works

To start each challenge, click the **“View Site”** button in the top-right corner of the task page. You’ll need to press this button **again for every new task**, as each one loads its own challenge site. Once clicked, the room will open in a **split-screen view**, letting you follow the instructions on the left while interacting with the challenge on the right. This is where you’ll complete all of our interactive challenges to get you ready for this year's event!

---

## 2\. Challenge 1 — Password Pandemonium

![Task banner](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/6228f0d4ca8e57005149c3e3-1763127292315.png align="left")

## Password Pandemonium

As you log into your new TBFC workstation, an alert pops up:

> “*Weak passwords detected on 73 TBFC accounts!*”

Even McSkidy’s password, `P@ssw0rd123`, has been flagged. Before gaining full access, you’ll need to prove your password prowess.

Strong passwords are one of the simplest yet most effective defences against cyber attacks.

**Objective:**  
Create a password that passes all system checks and isn’t found in the leaked password list.

**Steps:**

1. Enter a password with at least 12 characters.
    
2. Include uppercase, lowercase, numbers, and symbols.
    
3. Ensure it isn’t in the breach database.
    

#### My Solution: 1234P@assw0rd123

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1764599305491/a418c9a4-66eb-40de-a2f3-d1c657ff21d7.png align="center")

---

## Challenge 2 — The Suspicious Chocolate.exe

![Task banner](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/6228f0d4ca8e57005149c3e3-1763127337148.png align="left")

## The Suspicious Chocolate.exe

A shiny USB labelled **“SOCMAS Party Playlist”** appears on your desk. Inside is a mysterious file called `chocolate.exe`.  
It looks festive, but who sent it?

In this challenge, you’ll scan the file using a simulated VirusTotal tool to decide whether it’s safe or malicious.  
Checking suspicious files is a crucial skill for every defender.

**Objective:**  
Determine if `chocolate.exe` is safe or infected.

**Steps:**

1. Click the “Scan” Button.
    
2. Review the scan report (49 clean results, 1 malicious).
    
3. Decide correctly whether the file is safe or dangerous.
    

#### Solution:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1764599551542/dcaecae5-354f-426e-9363-2fc2b79f777d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1764599561274/9562f7fb-5163-4649-ad70-d990f756578f.png align="center")

---

## Challenge 3 — Welcome to the AttackBox!

![Task banner](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/6228f0d4ca8e57005149c3e3-1763127385113.png align="left")

## Welcome to the AttackBox!

You step into TBFC’s **AttackBox**, a secure virtual environment built for training. The system hums quietly, waiting for your first command.

This is where defenders learn, break, and rebuild safely. Getting comfortable with the command line is your first step toward cyber mastery.

**Objective:**  
Find and read the hidden welcome message inside your AttackBox.

**Steps:**

1. Use `ls` to list files.
    
2. Use `cd challenges/` to change directories.
    
3. Use `cat welcome.txt` to read the text file.
    

#### Solution:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1764599734515/7e600b0c-ba57-430d-afcd-e89b9d3e6fd6.png align="center")

---

## Challenge 4 — The CMD Conundrum

![Task banner](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/6228f0d4ca8e57005149c3e3-1763127496266.png align="left")

## The CMD Conundrum

McSkidy’s workstation shows signs of tampering, suspicious files moved, logs wiped, and a strange folder named `mystery_data`.

It’s time to use the **Windows Command Prompt** to uncover what’s hidden.  
Learning these commands helps you investigate systems and find what the GUI can’t.

**Objective:**  
Find the hidden flag file using Windows commands.

**Steps:**

1. Use `dir` to list visible files.
    
2. Try `dir /a` to reveal hidden ones.
    
3. Use `type hidden_flag.txt` to read the flag.
    

#### Solution:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1764600055857/faaaeb4a-b69e-4c28-8417-db75e3293ae8.png align="center")

---

## Challenge 5 — Linux Lore

![Task banner](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/6228f0d4ca8e57005149c3e3-1763127544173.png align="left")

## Linux Lore

TBFC’s delivery drones are glitching, dropping eggs instead of presents! McSkidy’s last login came from a Linux server, and something in his account might explain why.

Linux powers most servers worldwide, and knowing how to search within it is a must for any defender.

**Objective:**  
Locate McSkidy’s hidden message in his Linux home directory.

**Steps:**

1. Use `cd /home/mcskidy/` to enter his folder.
    
2. Run `ls -la` to show all files.
    
3. Use `cat .secret_message` to reveal the flag.
    

#### Solution:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1764600176769/90828731-94e2-452c-a1d3-337c750a7bad.png align="center")

---

## Challenge 6 — The Leak in the List

![Task banner](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/6228f0d4ca8e57005149c3e3-1763127586717.png align="left")

## The Leak in the List

Rumours swirl that TBFC’s data has been leaked. Emails are bouncing, and the staff are panicking.  
McSkidy suspects his account might have been part of a breach.

Defenders often use tools like **Have I Been Pwned** to check for compromised accounts. Early detection can stop an attack from spreading.

**Objective:**  
Check if McSkidy’s email has appeared in a breach.

**Steps:**

1. Enter [`mcskidy@tbfc.com`](mailto:mcskidy@tbfc.com) into the breach checker.
    
2. Review results for each domain.
    
3. Identify the one marked “Compromised.”
    

#### Solution:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1764600272865/2da3391e-dfa2-444c-ae29-3298d29068d4.png align="center")

---

## Challenge 7 — WiFi Woes in Wareville

![Task banner](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/6228f0d4ca8e57005149c3e3-1763127645725.png align="left")

## WiFi Woes in Wareville

The TBFC drones are looping endlessly over Wareville Square. Someone logged into the company router using default credentials!

Securing WiFi is critical. Default passwords are like leaving the front gate wide open.

**Objective:**  
Log into the router and secure it with a strong new password.

**Steps:**

1. Log in with username `admin` and password `admin`.
    
2. Go to “Security Settings.”
    
3. Set a new strong password that passes validation.
    

#### My Solution : `123P@ssword123`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1764600487704/5c4f23a7-f9dc-4b9f-915a-8800634d1453.png align="center")

---

## Challenge 8 — The App Trap

![Task banner](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/6228f0d4ca8e57005149c3e3-1763127690848.png align="left")

## The App Trap

McSkidy’s social account has gone rogue, posting strange messages about “EASTMAS.” A suspicious third party app may be behind it.

Learning to review and manage app permissions helps stop data leaks before they start.

**Objective:**  
Find and remove the malicious connected app.

**Steps:**

1. Review the list of connected apps.
    
2. Look for one with unusual permissions (like “password vault” access).
    
3. Click “Revoke Access.”
    

#### Solution:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1764600654182/db8af2d0-4927-470b-96cc-8f90710b4ede.png align="center")

---

## Challenge 9 — The Chat bot Confession

![Task banner](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/6228f0d4ca8e57005149c3e3-1763127752452.png align="left")

## The Chatbot Confession

TBFC’s AI assistant, **FestiveBot**, was meant to help write cheerful emails, but it’s been spilling secrets.  
Some messages reveal internal URLs and even passwords.

AI tools can be powerful, but defenders must know how to prevent them from oversharing.

**Objective:**  
Identify which chatbot messages contain sensitive information.

**Steps:**

1. Read each line of the conversation.
    
2. Select the ones containing private data.
    
3. Submit your findings.
    

#### Solution:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1764601001286/e11e1c44-b783-4714-91ed-068102d96ebf.png align="center")

---

## Challenge 10 — The Bunny’s Browser Trail

![Task banner](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/6228f0d4ca8e57005149c3e3-1763127781498.png align="left")

## The Bunny’s Browser Trail

SOCMAS web servers are showing heavy traffic, but one log entry stands out:

> “*User Agent: BunnyOS/1.0 (HopSecBot)*”

Someone or something has infiltrated the system.  
User Agent strings help defenders spot automated or suspicious visitors in network logs.

**Objective:**  
Find the unusual User Agent in the HTTP log.

**Steps:**

1. Read the provided web log entries.
    
2. Compare them to common browsers (Chrome, Firefox, Edge).
    
3. Identify and select the suspicious entry.
    

#### Solution:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1764601122067/5c11b7f4-c477-4de0-ac44-989bab5e3d2b.png align="center")

---

## The FINISH Line

## Consider Yourself Warmed Up!

Well done for making your way through Advent of Cyber 2025's Prep Track! These mini challenges have been designed to familiarise you with some of the key tricks and tools you'll need at your disposal to **help save SOC-mas** in this year's event. If you're looking to start your cyber security journey, there's no better place to do it than with us, as we take you on a tour of topics from **Linux CLI** to **Prompt Injection**, getting you up to speed with the world of cyber and all, while earning chances to win some of our amazing prizes in our annual AoC giveaway!  
  
Sounds like fun? It is! And you can wait for the fun to begin at this year's [**Advent of Cyber landing page**](http://tryhackme.com/adventofcyber25)**!**