---
title: "First time Setting Up n8n Self-Hosted on Docker"
seoTitle: "Guide: Setting Up n8n on Docker"
seoDescription: "Learn how to set up and automate workflows using n8n self-hosted on Docker for seamless social media integration and scheduling"
datePublished: Tue Nov 11 2025 11:32:27 GMT+0000 (Coordinated Universal Time)
cuid: cmhuhrtvf000402jmdrwkc6gq
slug: first-time-setting-up-n8n-self-hosted-on-docker
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1762860146373/222efcdf-abdf-43ef-a33b-aa3dea85e32e.png
tags: news, docker, automation, cybersecurity, cybercrime, n8n

---

---

### What is n8n?

n8n is a powerful workflow automation tool — think of it like an open-source Zapier. It lets you connect APIs, automate tasks, and even build custom integrations — all visually.

n8n is easy to use and probably has become one of my favorite tools of all time.

### Why i decided to start automating and for what?

As i work for my company, ***Yeti Cyber Operations,*** a startup i started with three other amazing individuals, i wanted us to have less load on posting things on social media to gain exposure, so i came up with the idea to automate not only our discord messaging but also linkedin posting mechanism.

---

## Part I

## Here is how i setup n8n as a docker instance

I started by spinning up a self-hosted n8n container with a persistent volume so that data and workflows stay intact even after reboots.

```bash
docker run -d \
  --name n8n \
  --restart unless-stopped \
  -p 5678:5678 \
  -e GENERIC_TIMEZONE="Asia/Kathmandu" \
  -e TZ="Asia/Kathmandu" \
  -e N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=true \
  -e N8N_RUNNERS_ENABLED=true \
  -v n8n_data:/home/node/.n8n \
  docker.n8n.io/n8nio/n8n
```

This creates a persistent volume (`n8n_data`) so my workflows remain saved even after reboots.

To start it again after reboot, just do:

```bash
docker start n8n
```

To stop after you are done with the day or you don’t have a separate server which is running 24/7 like me (i really need a serverrrr), you can:

```bash
docker stop n8n
```

By the way, after spinning up the docker instance make sure to check if the container was created and is running or not:

```bash
docker ps
```

---

## Part II

## Scheduling Automations in n8n

n8n comes with a **Cron node** for scheduling workflows.

Here’s what I did:

1. Created a new workflow
    
2. Added a **Cron** node to trigger the workflow at fixed intervals (for example, every morning at 7:00 AM)
    

```bash
0 7 * * *
```

It looks like this:  

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762860190925/b3a5efe8-773f-4450-a9c4-618f27e046a0.png align="center")

3. Then i connected the RSS feed, where i used ***The Hacker News RSS \` https://feeds.feedsburner.com/TheHackerNews\`*** data to fetch the articles.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762860245010/f27050a7-7762-461f-8f19-9aa68e88fae2.png align="center")

4. Then, I connected an If node , which extracted only the latest news, from current day.
    

Here is the condition script:

```javascript
{{ new Date($json.isoDate).getTime() }} is greater than {{ new Date(new Date().getTime() - 24*60*60*1000).getTime() }}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762860290955/952c661d-7b61-4896-b1dd-07dcd3aca847.png align="center")

5. After extracting, it conveniently gets saved in my Google Sheets.
    
6. Then I connected a Code node, which lets us write Custom JavaScript or Python code, as for mine, i wrote a script that filters out the duplicates, convenient right?
    

```javascript
// Get all input items
const items = $input.all();

// Keep track of GUIDs we've seen
const seenGuids = new Set();

// Filter items dynamically
const filtered = items.filter(item => {
  if (seenGuids.has(item.json.guid)) {
    return false; // skip duplicates
  } else {
    seenGuids.add(item.json.guid);
    return true; // keep new
  }
});

// Return in n8n format
return filtered.map(item => ({ json: item.json }));
```

7. Then finally, i connected my discord account and my news channel of **Yeti CyberOps Discord.** It requires you to create a discord app, a custom bot and add some credentials to finally run it.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762860352427/649c7065-a9e2-487a-8600-4471b083700b.png align="center")

7. Same goes for Linkedin, you have to go to Linkedin developer platform , create an app and finally, connect your personal or organization account!
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762860394459/4a25d506-c78f-4bc4-968b-6e4fe5726831.png align="center")

You can find many tutorials on the web, i am too lazy to find them again and paste their links here, sorry about that :P.

## Results:  

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762860631109/05a70883-d59e-4f31-b461-53e7f49b0127.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762860648793/f4260d45-6fc6-406a-9373-132acd980769.png align="center")

# What i learned

1. ### Always, i mean always, make sure your docker persists even after reboot, i had a heart failure when my laptop was cut off of power after it’s charge went out, fortunately, i still had my data even though i had to create a new docker instance.
    

# What i plan to do next

I really hope to connect my SIEM tool like Wazuh to automate the alert system, i am a sucker for SIEM tools after all.

Setting this up on Linux was a fun weekend project, i hoped the weekend had 3 more days but well, i managed to pull it off. See ya in my next article!