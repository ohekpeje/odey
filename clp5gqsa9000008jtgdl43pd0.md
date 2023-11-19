---
title: "BelkaCTF #2: Drugdealer Case"
datePublished: Sat Nov 18 2023 22:00:00 GMT+0000 (Coordinated Universal Time)
cuid: clp5gqsa9000008jtgdl43pd0
slug: belkactf-2-drugdealer-case
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1699210002790/af058a37-9034-4fdc-a32d-d46fb6b9d196.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1699210033103/f497cf0e-577f-4dbb-8dce-2813c636a2b1.png
tags: ctf, ctf-writeup, cyberforencsic

---

**Direct**: [dl.spbctf.com/BelkaDayUS\_CTF\_IMAGE.7z](http://dl.spbctf.com/BelkaDayUS_CTF_IMAGE.7z)

**Torrent**: [dl.spbctf.com/BelkaDayUS\_CTF\_IMAGE.7z.torrent](http://dl.spbctf.com/BelkaDayUS_CTF_IMAGE.7z.torrent)

**Archive password**: CwMglC7pLRHSkIlwoSqA

Loading the image on Magnet we can observe that we have 7769 evidence to analyze. I have also adjusted the time zone to get accurate results on my findings.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700395977446/f464576b-a812-417d-bb3a-342ae25807a1.png align="center")

**What is the full name of the phone owner? Format: First Name Last Name.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700396027037/7b2cf684-ed87-4c0d-93a5-81b5529f56c3.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700396067800/ce459ded-ce60-47ef-b1f3-dfdfde2d10b1.png align="center")

**Derek Hor**

**What is the phone number he reported to about drug delivery?**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700396119277/4960aab3-2727-46f1-a57e-caf10b9b59bc.png align="center")

Downloading and opening the contacts2.db file on Visual Studio loads like the file is corrupt even though you will find the contact details

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700396151914/4b3d57bf-cde9-45ab-b93c-3a91b1269189.png align="center")

However, searching for the phone number on the Autopsy tool is very straightforward as the forensic tool is able to show the contact number.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700396217119/a8a5c4bc-84b4-4b2b-a2eb-9521156c6a30.png align="center")

**+12395104974**

**What were the suspect’s delivery locations on the night of arrest?**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700396340830/0d760c7e-a14a-4017-83db-80cba67cda38.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700396383373/a1d44fec-3e62-43ca-a3db-fa8e60bfe862.png align="center")

**Camelback Golf Club, 7847 N Mockingbird Ln, Scottsdale, AZ (33.5542226,-111.9340928)**

**2013 W Harwell Rd., Phoenix, AZ (33.374304,-112.1035501)**

**33°29'04.2"N 111°52'38.0"W (33.4845,-111.877215)**

**How long has the suspect been acting as a drug dealer?**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700396438987/98720fae-78dd-4cb9-ac0c-9049dacb0a09.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700396460258/377bec17-0cf5-4693-9f66-ad3a647dbce5.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700396485343/9e94652c-8c3c-4657-8ad5-95538333312c.png align="center")

**303 days**

**From what Bitcoin wallet did he get paid the last time for his job?**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700396623414/52fbf189-8335-4192-b5aa-8c931d4ea3ed.png align="center")

Searching the Bitcoin addresses on the blockchain provides 3 results

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700396664907/e5201824-a488-4640-8b2e-92061c01c5dd.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700396691063/a925b472-96fd-48d7-813f-a883d87f1629.png align="center")

**113JqY3CqsQPT7EN6wj5tRAVKftEP9rQC**

**What is the phone number of the drug supplier?**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700396745555/1a9b15b7-189e-4353-ae15-7d6e511938f0.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700396782639/aface599-0896-4688-9f5b-af414dc1cc15.png align="center")

1\. After locating the Signal backup (manually) and the password (any SQLite viewer, this time you do not need WAL or freelist support), you can use an open source tool [https://github.com/pajowu/signal-backup-decode](https://github.com/pajowu/signal-backup-decode) as follows:

/root/.cargo/bin/signal-backup-decode --password '04049 19810 47697 72485 91554 88046' signal-2020-12-20-21-04-59.backup

2. The tool creates an SQLite database with the extracted data. In the 'recipient' table we see two phone numbers: +13148346839 corresponding to profile name horatio0.42k (it's Derek Hor), and +14233767293 which is our target supplier

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700396886767/be059122-b9f8-4164-b486-1b24482b841f.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700396911765/f4356d51-de8a-4afb-bb3a-8d735b7a9b97.png align="center")

**+14233767293**

**When was the last time the suspect met his supplier? Provide exact timestamp in a common format, e.g. 2021-07-17 17:07:07 UTC**

1. This time we can use the Signal message history extracted. There we see that there was a meeting planned for Dec 17th at 2 PM, and the planned location was 33.508136, -112.148462

2. Alas, this was not the last meeting with the supplier. False lead! Well, almost...

3. If we look at the Calendar, we can find 33.508146, -112.148462 location for one of the events, for 2020-12-17 at 21:00:00 UTC (it is 2 pm Phoenix time)

4\. Select this event and switch to the SQLite view of the Calendar. The title of the event is 'Pizza delivery':

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700397084788/a427bc22-a3e0-4211-841a-25dba7eca81c.png align="center")

Converted the epoch time format to UTCM Unix time online tool: [https://www.epochconverter.com/](https://www.epochconverter.com/)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700397128043/17b2d40c-68fe-41f1-8399-be18cbedada2.png align="center")

**Sat, 10 Apr 2021 07:30:00 UTC**

**What is the supplier's phone IMEI identifier? Help yourself to the NSA metadata storage:** [*cellrecordslookup.nsa.fyi*](http://cellrecordslookup.nsa.fyi)

*Sun, 28 Jun 2020 00:00:00 -0700 33°32'56.2"N 112°06'22.5"W*

*Wed, 02 Sep 2020 11:00:00 -0700 33°32'16.4"N 112°07'11.9"W*

*Thu, 17 Dec 2020 14:00:00 -0700 33.508146, -112.148462*

***Tue, 29 Dec 2020 14:00:00 -0700 33.528795, -112.071941***

*Tue, 16 Mar 2021 15:20:00 -0700 33.54730553325095 (bad location)*

*Sat, 10 Apr 2021 00:30:00 -0700 33.529455426023574, -112.0847381568517*

1. For this task, we were given an 'NSA' tool that allows us to look up cellphone registration history. When we look at the tool, we see we need a latitude, longitude, and a date in (MST). Now we must enter the data. Take the data extracted from the Calendar automatically by Belkasoft X or manually by yourself

2. Feed every line into the lookup tool. You will get the output of the number of devices found with their IMEIs. Copy the list of IMEIs into an Excel spreadsheet. You can intersect all the lists by duplicate search (meaning that an IMEI was found in more than one location). Just two IMEIs will be common for all the locations, they are 350236009513272 and 332182208414842. One of those is Derek, the other is the supplier

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700397200354/b4645a5c-7a60-4869-a83d-00ffe8cea66a.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700397260595/54ab8001-332f-41e1-a52b-0cbed7835720.png align="center")

**Tools used:** Magnet Axiom, [epochconverter.com](http://epochconverter.com), VS code application, Autopsy, [www.timeanddate.com/date](http://www.timeanddate.com/date), [blockchair.com/bitcoin/outputs](http://blockchair.com/bitcoin/outputs), [cellrecordslookup.nsa.fyi](http://cellrecordslookup.nsa.fyi)

**Resource**

[CTF | Belkasoft](https://belkasoft.com/ctf_may/)