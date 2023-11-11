---
title: "BelkaCTF #4: Kidnapper Case"
datePublished: Sat Nov 11 2023 12:08:45 GMT+0000 (Coordinated Universal Time)
cuid: clou06tf1000009l5gqc85wez
slug: belkactf-4-kidnapper-case
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1699208944961/0fd1ee9f-1a9d-4257-bc10-da002c76f8db.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1699210055292/2901f1a7-0400-4335-adc7-6a70b5c69449.png
tags: ctf, ctf-writeup, cyberforensic

---

I performed and completed this challenge in 2002 for a coursework in Cyber Forensics, just coming around to uploading it on my blog in 2023.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699204992637/b2d02acc-f6cc-4e42-a3bc-b979c63cc222.png align="left")

***List all users of the laptop***

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699205039563/5f12c32c-decf-4e96-b5af-25fd5aa808da.png align="left")

**What web application was used by the boy to earn his pocket money?**

A simple scan of the Firefox web history indicates several hits for [x-tux-0.web.app](http://x-tux-0.web.app). There are some intriguing goods for sale, as we can see.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699205075578/1773d425-b774-4ee6-8ae8-cb4b5d35e428.png align="left")

Open **places.sqlite** with Visual studio SQL Lite and you will find the web application.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699205096371/a807e4d2-d035-4879-baa1-cccb30278836.png align="left")

**Which BTC wallet did the boy use to sell drugs?**

Visiting the link for the above task [**https://x-tux-0.web.app**](https://x-tux-0.web.app) you will access the drug dealer's business page with his wallet address.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699205141629/c863d2b5-ddec-493c-9ffd-1a9dc09d06db.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699205163772/7dd8c9aa-2537-4661-b767-18fab9fdbadd.png align="left")

**On which date does the kid's database show the most sales for "Acapulco Gold"?**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699205188801/aad2bb2e-ecac-4268-86bb-ee5b91e06908.png align="left")

There are several talks from a "Tux" with the subject "Sell Database" after going through email communications.

In the chat, the victim asks his friend Tux for his monthly sales, most likely to keep track of his drug supplies and the money he makes from his sales.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699205214289/62eb2cf4-b4f6-4266-80b3-e5e5be078958.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699205236344/c31c0eff-902e-449a-ba18-9aaeb72899d6.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699205259177/bde0617a-b951-4c8f-9be6-df055c8af98c.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699205419130/08732bb7-df05-4d24-b546-8715b31891df.png align="left")

As seen in the image above, the dictionary attack was successful and the password was **vondutcemonaheem gangsta78**. The zip file was cracked using Passware Kit Forensic and the 10-million-password-list-top-1000000.txt file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699205441973/0b00230d-5b89-45b2-a5de-61ba4b79c068.png align="left")

We can see two folders for different years. Each folder contains Excel documents and after going through each one of them we can see the month with the most sales.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699205468028/e46d75e8-fd21-42e4-bd1a-c68c3271e3b3.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699205487899/a5b2e9e6-bddd-40e6-a9d5-8f73e405e439.png align="left")

**What was the other BTC wallet of the victim, which he used to hide his "under the counter" sales from his superior?**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699205508907/b9cc8f79-5c1c-4801-8df8-493d8124847e.png align="left")

*Before changing first 4 bytes*

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699205530410/2f80997e-18a8-40e2-8af3-dd1097d36a57.png align="left")

*Replace the first 4 bytes on the file titled "101.bin" to a PDF header "25 50 44 46" and the document will show up as an invoice.*

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699205718673/3ce3556f-f3cc-4254-b85b-5d7531eea0f5.png align="left")

*Saving converted .bin file to .pdf.*

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699205748435/f08f6ca5-f889-488e-8626-ecf5b4f6789d.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699205769120/b0034d67-c3cf-4174-a969-cafcf7c43763.png align="left")

**What is the password to the boy's notes?**

You had to locate both the note itself and the password for it in order to answer this two-part question. Fortunately, locating the memo was simple (sort of). More file system exploration led me to the following path:

*/img BelkaCTF Kidnapper Case.E01/vol vol6/home/stanley/Documents/.mynote*

There were two files inside: "notes" and "mynote.odt" (extensionless). The first one was uninteresting, but the second felt strange due to the absence of an extension. It appeared promising that this was what I was supposed to be looking for when I attempted to access it in Microsoft Word and was prompted for a password.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699205820412/61a6d1d7-636e-4f40-b65f-1ba4b20de96b.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699205839365/9856a0f0-9d72-49c2-8463-b6ee4fd1416c.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699205866666/a21965b5-1527-48cb-bc9b-ba639e773d01.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699205893356/66079627-0c6c-4725-82b4-ae006ae23ef1.png align="left")

Throw the file into an online tool like **Cyberchef** and decrypt it using "**from Base32**" and "**Rot13**". All passwords are displayed.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699205916841/cc48991e-4bb1-42db-a382-681b0363b9ed.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699205936969/6982b4f2-b95e-4e54-9891-cbab97fb80ff.png align="left")

*Use the password above to open the notes file.* **"!mp0rt4nTNot3"**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699205959009/72db6092-30c8-4225-8ef8-e7239da79fa1.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699206165125/5b3927d5-13df-46e6-a1bd-799dc825eae8.png align="left")

***What is the "secret pin" mentioned in the notes?***

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699206188698/18594eee-6162-4ff9-9e0a-a1d70fc3093a.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699206230418/99af8d95-692c-40c8-a576-acd2f0fcc785.png align="left")

Opening the file in Wireshark we can look for any packets of interest. We see some HTTP GET requests for a file called "vault\_secret\_code.wav".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699206258736/bbf02683-e649-492c-8316-dea777d7f2d6.png align="left")

Notice the audio/wav record that became located in the PCAP record. Export this record and try and play it with a general audio/mp3 participant. You will notice, it's far truly an audio record with no significant sound inside, so that you can require a few kinds of spectrum analyzers. Using a free online tool //[www.dcode.fr/spectral-analysis](http://www.dcode.fr/spectral-analysis). Load the record into this and you will see the message.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699206287047/7a041df2-ac78-4519-a49b-1f53a7f1693e.png align="left")

Fortunately, "[Connections.zip](http://Connections.zip)," another file contained inside "[mycon.zip](http://mycon.zip)," was not password-protected. There was a "Sheet1.html" file within that had a complete list of names and email addresses. We figured Tux was definitely the bad guy, so I quickly searched the text.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699206316004/782248ab-264e-4a1e-9166-9553c8d9ebef.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699206362340/335fd5ab-7a50-4164-96f0-3bceb8b9981d.png align="left")

**When did the boy receive a threat?**

Since I had already located the "notes" file, this problem was essentially solved. Even though a timestamp is already visible in Unix Epoch, you must read the entire post to fully get the context of the question and the desired response.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699206407553/4271dad1-941e-4d62-88f4-709e22c4172d.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699207281033/1269bb57-9171-4144-9392-044786b9a0b9.png align="left")

**Who was the kidnapper?**

There was a "Sheet1.html" file within that had a complete list of names and email addresses. We figured Tux was definitely the bad guy, so I quickly searched the text.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699207356333/3e540f93-c947-4b17-a0ed-4d9e39764ee1.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699207374738/00f18998-1dee-40e4-a4ad-9d870b432bfe.png align="left")

**Tools used**: Magnet Axiom, Cyberchef, John the Ripper, Wireshark, dcode, [hexed.it](http://hexed.it), Passware Kit Forensic, Autopsy

### Resource

[BelkaCTF (](https://belkasoft.com/ctf)[belkasoft.com](http://belkasoft.com)[)](https://belkasoft.com/ctf)