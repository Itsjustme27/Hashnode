---
title: "Word Sea Adventures Writeup"
datePublished: Sun Nov 23 2025 18:01:11 GMT+0000 (Coordinated Universal Time)
cuid: cmic0xz5g000102lbgtc5e1di
slug: word-sea-adventures-writeup
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1763956346326/a1ce9f18-893d-439a-bd43-5df25faba5cd.png
tags: cybersecurity, ctf, forensics, word-document

---

> Challenge Description:
> 
> Our experts found this weird word document in our file share. They couldn't find anything inside. Maybe you could look more closely and find the hidden prize within!
> 
> No passphrases are needed for this challenge.
> 
> The flag format will be tctf{flag} or pctf{flag}
> 
> Challenge author: DJ Strigel

When I first downloaded a mysterious file called `word_sea_adventures.docx`, I honestly expected one of those standard steganography traps. You know — hide an image in `/word/media`, embed a secret in document.xml, maybe some Base64 somewhere.  
But nope. This one turned out way cleaner and way more evil.

This is a full write‑up of how I solved the challenge and found the hidden **tctf{} / pctf{}** flag — and what I learned along the way.

## **Step 1: Treat DOCX Files as ZIP Archives**

One thing every forensics enthusiast should remember:

> **DOCX = ZIP archive. Always unzip it first.**

So I started with:

```bash
$ binwalk word_sea_adventures.docx

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             Zip archive data, at least v2.0 to extract, compressed size: 387, uncompressed size: 1933, name: [Content_Types].xml
464           0x1D0           Zip archive data, at least v2.0 to extract, compressed size: 231, uncompressed size: 722, name: _rels/.rels
764           0x2FC           Zip archive data, at least v2.0 to extract, compressed size: 973, uncompressed size: 2383, name: word/document.xml
1812          0x714           Zip archive data, at least v2.0 to extract, compressed size: 260, uncompressed size: 1203, name: word/_rels/document.xml.rels
2158          0x86E           Zip archive data, at least v2.0 to extract, compressed size: 109, uncompressed size: 124, name: word/_rels/footnotes.xml.rels
2354          0x932           Zip archive data, at least v2.0 to extract, compressed size: 333, uncompressed size: 1701, name: word/numbering.xml
2763          0xACB           Zip archive data, at least v2.0 to extract, compressed size: 2249, uncompressed size: 21408, name: word/styles.xml
5085          0x13DD          Zip archive data, at least v2.0 to extract, compressed size: 278, uncompressed size: 843, name: word/footnotes.xml
5439          0x153F          Zip archive data, at least v2.0 to extract, compressed size: 217, uncompressed size: 625, name: word/comments.xml
5731          0x1663          Zip archive data, at least v2.0 to extract, compressed size: 285, uncompressed size: 583, name: docProps/core.xml
6091          0x17CB          Zip archive data, at least v2.0 to extract, compressed size: 356, uncompressed size: 724, name: docProps/app.xml
6521          0x1979          Zip archive data, at least v2.0 to extract, compressed size: 136, uncompressed size: 212, name: docProps/custom.xml
6734          0x1A4E          Zip archive data, at least v2.0 to extract, compressed size: 1561, uncompressed size: 7674, name: word/theme/theme1.xml
8374          0x20B6          Zip archive data, at least v2.0 to extract, compressed size: 583, uncompressed size: 1409, name: word/settings.xml
9032          0x2348          Zip archive data, at least v2.0 to extract, compressed size: 156, uncompressed size: 199, name: word/webSettings.xml
9266          0x2432          Zip archive data, at least v2.0 to extract, compressed size: 411, uncompressed size: 2494, name: word/fontTable.xml
9753          0x2619          Zip archive data, at least v2.0 to extract, compressed size: 104693, uncompressed size: 144327, name: crab.jpg
114512        0x1BF50         Zip archive data, at least v1.0 to extract, name: docProps/
114579        0x1BF93         Zip archive data, at least v1.0 to extract, name: _rels/
114643        0x1BFD3         Zip archive data, at least v2.0 to extract, compressed size: 233483, uncompressed size: 274007, name: sponge.jpg
348194        0x55022         Zip archive data, at least v2.0 to extract, compressed size: 207034, uncompressed size: 376280, name: squid.jpg
555295        0x8791F         Zip archive data, at least v1.0 to extract, name: word/
555358        0x8795E         Zip archive data, at least v1.0 to extract, name: word/_rels/
555427        0x879A3         Zip archive data, at least v1.0 to extract, name: word/theme/
557545        0x881E9         End of Zip archive, footer length: 22
```

Lots of file here huh, The ones which caught my eyes were definitely the image files, crab.jpg, sponge.jpg, squid.jpg.

Since the binwalk command i used without the extract flag only displays what was hidden, so i extracted it using another tool called, unzip, since it’s literally just a zip file.

```bash
$ unzip word_sea_adventures.docx -d docx_contents
```

This is what the contents of the docx\_contents looked like:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1763918394321/0ccfa11e-25d8-4e2c-8fe2-73b5e45256ad.png align="center")

Images huh, i immediately thought it was suspicious, and checked it’s exif data to not find anything, so i just simply used steghide to extract it (after i asked chatgpt what to do next lol)

I choosed the first file just to check and got the biggest hint:

```bash
┌──(itsjustme㉿kali)-[~/Downloads/patriotctf/docx_contents]
└─$ steghide extract -sf crab.jpg          
Enter passphrase: 
wrote extracted data to "decoy2.txt".
                                                                                                                                                                      
┌──(itsjustme㉿kali)-[~/Downloads/patriotctf/docx_contents]
└─$ ls
'[Content_Types].xml'   crab.jpg   decoy2.txt   docProps   _rels   sponge.jpg   squid.jpg   word
                                                                                                                                                                      
┌──(itsjustme㉿kali)-[~/Downloads/patriotctf/docx_contents]
└─$ cat decoy2.txt  
Mr Crabs heard that his cashier may be hiding some money and maybe a flag somewhere.
```

Oooooh big reveal, Mr Crabs’ cashier huh, since i haven’t watched spongebob that much, so i googled who the cashier was and it was none other than Squidward! whose image was in the content, so without wasting any time, i extracted it as well and got the flag!

```bash
┌──(itsjustme㉿kali)-[~/Downloads/patriotctf/docx_contents]
└─$ steghide extract -sf squid.jpg
Enter passphrase: 
wrote extracted data to "flag.txt".
                                                                                                                                                                      
┌──(itsjustme㉿kali)-[~/Downloads/patriotctf/docx_contents]
└─$ cat flag.txt  
I guess you found handsome squidward... even his looks can't hide the flag.
tctf{w0rD_f1le5_ar3_als0_z1p}
```

All and all, it was a fun and easy forensics challenge, i enjoyed it!