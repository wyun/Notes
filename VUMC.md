# Oracle Related Topics

## Setup .cshrc file
`setenv LD_LIBRARY_PATH /usr/openwin/lib:... ... ... :/home/ICoracle`

## How to use Cursor?

http://www.dba-oracle.com/t_dbi_perl_lob_large_objects.htm

A few key points:
- $csr is a cursor type.  It needs to be defined as such.
- Fetch results using $csr instead of $sth.
- use DBD::Oracle qw(:ora_types);   # need this line to define cursor types

## Example script to Vandyworks / WorkBrain's stored procedure
`stardev4:/home/httpd/webhome/cgi-bin/wangy9/top/testWorkBrain`

# StarPanel Resource Account

email: star.p.aai.user@vumc.org
We got this notification about the resource account **aaiusesp** expiring.  We searched on Pegasus and didn’t find a proper place to renew it.  Do you know the proper way to send this renewal request?
 
The resource account is used by StarPanel for LDAP, OnBase, etc.

Trisha's email: 
Can you please submit the following Pegasus ticket - https://pegasus.vumc.org/request/start/21/?s
 
Include the following information in the ticket: (The knowledge article for submitting information is here - https://pegasus.vumc.org/ViewKnowledge.aspx?id=21)
 
The VUnetID, the first and last name, and an external email address for the individual.
If this is a Resource or Test account, include the best notification email address.
The department (or school) under which the account is profiled. For example, Childrens Hospital, School of Engineering, etc.

Previous Ticket: https://pegasus.vumc.org/request/?id=R00614006
 

# Oracle tnsnames.ora file location
`\\celerra\psoft\oracle\admin\`

# Star Daily archive file
*Aug 11, 2017, 12:07 PM by Yun Wang*
```
com 31 ls -l /usr/star/archivian/star30/vault/vumc

or 

com 31 ls -l /usr/star/archivian/star34/vault/vumc
```

# SSO: SMART on FHIR / OAuth

*posted Mar 8, 2017, 10:07 AM by Yun Wang   [ updated May 24, 2017, 4:09 PM ]*

https://confluence.mc.vanderbilt.edu/display/~coffmata/Embedding+an+external+web+application


> From Jason Minton:
> 
> Internal: https://ic1-np.service.vumc.org/Interconnect-POC-FHIR/
> 
> External: https://arr01-np.service.vumc.org/FHIR-POC/

There’s a ‘Developer View’ link on the Internal status page where you can find details on the available web services and how to call them.

FHIR isn’t yet configured for REL, but if it’s needed, we can work on it.


client ID in DEV environment: `bb311191-772f-46d7-9585-469e3973f620`


# Command Line on Epic

*posted Mar 3, 2017, 1:40 PM by Yun Wang   [ updated May 2, 2017, 3:54 PM ]*

`ssh epc11lt -t "/usr/bin/bash"`


Sync with virtual box
```
alias: pullcs2
rsync -azP -e  "ssh -p 37250" wangy9@stardev3.mc.vanderbilt.edu:/home/wangy9/cs2/bin /home/wangy9/Apps/epicleap

com 7 /usr/star/bin/starter start .II $afs/cs2/bin/epiclog-killc
```


# Epic - filing results to document interface
*posted Feb 7, 2017, 2:00 PM by Yun Wang*

Hi Yun,

We can file documents at the order and result level over the incoming transcription interface (99704101). There are some additional data that we should include for documents to be filed at this level:


-          ORC-1: Control code

o   Should be “RE”

-          ORC-16: Control code reason

o   Typically used for cancellations. If this is a cancel message, this field is required

-          OBR-1: [set id, increments]

-          OBR-3: Accession number

o   Used to uniquely identify results. (May also be received in OBR-20.)

-          OBR-4: Procedure ID

o   This is optional, but would be nice to have the EAP ID. For a conversion these can all map to the same procedure, defaulted in the extract

-          OBR-16: Ordering Provider

-          OBR-22: Report change timestamp (if applicable; this is recommended but optional)

-          OBR-25: Result status

o   Typically “F” for final on converted results

 
Here’s a sample of the format, red=required, yellow=recommended if available/applicable, green=optional.
```
ORC|<Control Code>|||||||||||||||<Control Code Reason>|

OBR|<Set ID>||<Accession Number>|<Procedure ID>||||||||||||<Ordering Provider>||||||<Report Change Timestamp>|||<Result Status>|
```
 

 
Are these data elements available out of Star? Please let me know if I can clarify anything.





# 常见nvm命令

ref: https://pengjiyuan.github.io/

1. 安装node：
nvm install <version>

nvm 默认是从 http://nodejs.org/dist/ 下载的, 国外服务器, 必然很慢, 好在 nvm以及支持从镜像服务器下载包, 于是我们可以方便地从七牛的 node dist 镜像下载:

NVM_NODEJS_ORG_MIRROR=https://npm.taobao.org/mirrors/node nvm install 5

5是5.xx版本的意思，6即是6.xx版本，也可以指定版本如5.9.1

2. 查看node版本
nvm ls

列出你安装的所有版本的node以及当前你所用的node版本，还有你默认的node版本。

3. 切换node版本
nvm use version

4. 设置默认版本
nvm alias default v5.9.0
  

# git安装及配置
  
1. 安装git
`$ sudo apt-get install git`
  
2. 配置git
`$ git config --global user.name "your name"`

`$ git config --global user.email "your email"`
  
3. 创建SSH Key
`$ ssh-keygen -t rsa -C "youremail@example.com"     `

`$ cd ~/.ssh`    可以看到id_rsa(私钥)和id_rsa.pub(公钥)，将id_rsa.pub的内容添加到    

GitHub->Account-settings->SSH Keys中
  
4. windows下配置git：
`$ Git config --global user.name "your name"    `

`$ git config --global user.email "your email"`
创建SSH Key:

不同于linux，window没有~/.ssh，需要生成秘钥到/c/Users/Administrator/.ssh。

进入/c/Users/Administrator/.ssh目录，ssh-keygen -t rsa -C "youremail@example.com" ,接下来同linux操作。

设置SSH自动登录：

`git remote set-url origin git@github.com:wyun/pluralsight-js-dev-env.git`


  
# Linux zip
`zip -r myfile.zip ./*` 将当前目录下的所有文件和文件夹全部压缩成myfile.zip文件,－r表示递归压缩子目录下所有文件.

`unzip unzip -o -d /home/sunny myfile.zip`
  
把myfile.zip文件解压到 /home/sunny/
-o:不提示的情况下覆盖文件；
-d:-d /home/sunny 指明将文件解压缩到/home/sunny目录下；

`zip -d myfile.zip smart.txt`
删除压缩文件中smart.txt文件
zip -m myfile.zip ./rpm_info.txt
向压缩文件中myfile.zip中添加rpm_info.txt文件

`zip -r filename.zip file1 file2 file3 /usr/work/school`
上面的命令把 file1、file2、 file3、以及 /usr/work/school 目录的内容（假设这个目录存在）压缩起来，然后放入 filename.zip 文件中。
  
  
  
  
# incr - Incremental file

  *posted Feb 21, 2013, 9:57 AM by Yun Wang   [ updated Feb 21, 2013, 9:57 AM ]*
To reload a patient's chart, use ~/rebuildadoc $mr $db 'train'||'test'

Or from script: 
queue_file(“/usr/star/dequeue/incremental-$db/rebuild-$mr”, $pseudofile, hostSet(‘incremental’, $lastDigitOfMR));
  

# 2011-2012 Work Summary

  *posted Apr 16, 2012, 10:46 AM by Yun Wang   [ updated Apr 25, 2012, 5:09 PM ]*
Project

ADVANCE project
Enhance ExternalLab data entry; New interface for admins to modify previous ExternalLab results, create new templates for clinics, simply process to correct erroneous lab value during data entry.
Priority Problems (create line display, indicators, dashboard)
Integrate StarPager with VUDirectory, greatly improve the pager database's accuracy, add more admin functions, create API to feed StarPager data to other systems, added more SMS providers.
RxStar dashboard integration with StarPanel
Interface for admins to create OPC templates.
ClinicSummary display and maintenance.
Switch patient ICD9 history to use PSS service.
Create ImageQueue folder function for MR Admins.
Merge functions of Admin and AdminDesign page.
Display more accurate information for users using cached data from LDAP
Created Immunization NDC mapping tool for AdminRx administrators to make sure all vaccines are imported properly into StarPanel.
Created function for Admins to create new tabs in TeamSummary, allow copy sections between TeamSummary tabs, allow copy PtSummary data into TeamSummary, add Primary Problem selector.
Enhance JS widgets such as Calendar, panel selector and filter, 
Display PCP information in yellow frame. Popup information window for printing.
Advanced patient search function.

## Area

 jQuery / JavaScript, SignDrafts, MyText, ExternalLab, StarPager, ICD9 update, Attestation, ImageQueue, TeamSummary, Panel,  Immunization Import from AdminRx, EDExpect form

2012-2013 GOAL #2 VPES Performance Evaluation

Rationalize display of all Star Documents; Provide library with report for document(s) displa, whether from code or data structures. Eliminate historical and obsolete code. 
  
# com run as HTTPD
posted Jan 2, 2009, 1:42 PM by Yun Wang
`/afs/vumc/usr/crab/xfer/dario/wex It supports things like wex -self command wex star12 star13 command`
  
#Generate USER id and provider code
posted Feb 11, 2009, 10:27 AM by Yun Wang   [ updated Apr 3, 2012, 4:19 PM ]
on sun15, 17, 19 running makeSPidcode
```
Source dir: /usr/star/par/census
Destination: /usr/star/data/public
```
  
# ADT HL7 message feed
posted Feb 11, 2009, 10:28 AM by Yun Wang
Running a service called "receiver" on sun16
it parses HL7 messages received via socket connection and process them in place.
  
  
# How Provider Code is generated.
posted Feb 20, 2009, 3:44 PM by Yun Wang   [ updated Jul 13, 2011, 3:31 PM ]
on Sun15: 
/usr/star/par/census/prepare-auth generated file is distributed to /usr/star/data/public/

  
# Dario's clue bag
 posted May 15, 2009, 9:37 AM by Yun Wang   [ updated Sep 15, 2009, 2:44 PM ]

  Dario's clue bag:

`/afs/vumc/usr/crab/xfer/dario/docs/clues`

# Local cache file location
posted Mar 3, 2009, 2:59 PM by Yun Wang
`/home/httpd/private/Cache/vumc/[checkdigit]/[fullmr#]`

The last file is HED data. Use emacs's search backward [Ctrl+R] to find that :adm: location and see all information related to HED.

# StarPanel Get a single document from cache
posted Jun 3, 2008, 3:25 PM by Yun Wang   [ updated Jul 27, 2011, 9:58 AM ]
`use Star; use Record; cache_request (\*S, "vumc", {mrn=>"010533644", uniq=>"713e9kag0"}, sub {while (<S>) {print}})'`

or 

`perl -e 'use MR; $a = get1uniq("000000840", "a26fuch00", "fooooo", "noMR"); print "$a\n";' 
and then open document 'fooooo'`

or 
`getUniq $mr $uniq [$db]`
  
# StarPanel Archive Location
posted May 30, 2008, 5:35 PM by Yun Wang
starpanel archive

all documents from the past 30 days are stored in sun31
/usr/star/archive/vumc/(dd)
dd is the date number

# Patient Cache Location
posted May 30, 2008, 5:35 PM by Yun Wang
StarPanel Cache Path: 
/usr/star/db/vumc/cache/(00..99)/xxxxxx
in 0 set servers
for 010533-64-4 
it's in sun0(4) 
directory (64) 
file   (010533)
server set: 0 4 5 6
  
  
# Kill an HTTPD process
  
posted May 30, 2008, 5:36 PM by Yun Wang
com -port 4038 startest1 kill -9 23504


# restart StarFire mod script
  
posted Jun 3, 2008, 10:54 AM by Yun Wang
/afs/vumc/usr/crab/xfer/dario/restCgi <scriptname>
 
The available scripts running as ongoing process are listed in StarFile.pm in ../cgi-bin/sp/ directory
  
  
# Deuniq
  
posted May 15, 2009, 9:38 AM by Yun Wang
reverse a unique ID generated from star: deuniq [uniqid]
(Edit post)
  
# use Discrete or other /usr/star/pm modules
posted Jun 29, 2009, 3:14 PM by Yun Wang
add

  `use lib "/home/httpd/webhome/cgi-bin/wangy9/top";`
to the top of the script.
  
# StarPanel access log

  posted May 19, 2009, 1:42 PM by Yun Wang
Access log is located at: 
/home/localweb/logs/ssl/access_log.#########

# Remote access SSH to StarPanel servers
posted Oct 22, 2008, 1:16 PM by Yun Wang
ssh wangy9@server -p 37250

Or call the server outland

ssh wangy9@outland.mc.vanderbilt.edu -p 37250
  
# Vanderbilt long distance phone network V-NET code
posted Jun 3, 2008, 3:28 PM by Yun Wang   [ updated May 15, 2009, 4:01 PM ]
Vanderbilt long distance phone network V-NET code

Name: Yun Wang
V-Net Code: 469-4125

Domestic Long Distance:
#9 + VNET CODE + 9 + 1 + area code + number

International Long Distance:
#9 + VNET CODE + 9 + 0 + 11 + country code + city code + number
  
  
# Star Monitoring
posted Jun 3, 2008, 4:18 PM by Yun Wang   [ updated Feb 4, 2010, 3:27 PM ]

startest6:/home/dario/bin/watch show all web servers' error log

startest1:/cgi-bin/surveillance show all processes running on other servers

Monitor: 

startest1 or sun14: quickmon on shell
Or webbased Star Monitoring: on https://startest1.mc.vanderbilt.edu/cgi-bin/mon/. Only on IE
snap: https://startest1.mc.vanderbilt.edu/cgi-bin/mon/snap.cgi

Big Brother:
http://earth.mc.vanderbilt.edu/bb4/www

Always use demo mode when present to groups, or use Spqr10

Update mysql to create mysql table to spqr10

Update release file with notes. Automatically send them to Dario with relnotify.pl

Always test code in all 3 browsers: IE, FireFox, chrome.


  
# LDAP

  *posted Sep 15, 2011, 4:04 PM by Yun Wang   [ updated Mar 3, 2015, 2:09 PM ]*
Server running: startest6

To loadLDAP data: 

Run loadVUusers.pl -all for all. or -offset n to load previous nth day's change.
To remove records with duplicate RACFID:  remDupLDAP.cgi  to show; remDupLDAP.cgi 1 to remove. 

To search records based on racfid or vunetid: ldap.cgi -racfid or -vunetid

To show all users with different pager numbers from LDAP's pager numbers. 
```
select ldap.racfid, displayname, phone, email, pagernumber, pagerconfirmeddate, pager, lastchange from user2pager right join ldap using (racfid) where ldap.pager !="" and user2pager.pagernumber != "" and ldap.pager != user2pager.pagernumber order by pagerconfirmeddate
select count(*) from user2pager right join ldap using (racfid) where ldap.pager !="" and user2pager.pagernumber != "" and ldap.pager != user2pager.pagernumber order by pagerconfirmeddate
```
Run pagerSync.cgi once in a while to get rid of entries with identical pager number in LDAP and StarPager.
_____________________
Yun,

The request has been approved. Please use the following settings:

ldaps://ldap.vunetid.mc.vannderbilt.edu:636

hostname:  ldap.vunetid.mc.vanderbilt.edu

Port 636

Use Simple bind with SSL

User base DN:   is ou=peoplne,dc=vannderbilt,dc=edu

 

connect using  uid=aaiusesp,ou=Special Users,dc=vanderbilt,dc=edu

password in .cshrc

contact person: Lee Brewer

 

You can now submit your request online at

https://its.vanderbilt.edu/partnerticket/

 

t  Partner Support

r  Information Technology Services

a  Vanderbilt University

e  (615) 936-4877

l  http://its.vanderbilt.edu/lsp-support

n P @ 5
  

# Update New STARPANEL system
posted Jun 3, 2008, 3:26 PM by Yun Wang   [ updated Jan 8, 2010, 5:11 PM ]
Update New STARPANEL system:
```
*.cgi
*.pm
*.js
*.html
*.htc
googie/*
theme/*
```

Make softlinks to other files by using the list generated from command "ls -F|grep @"
Mandatory soft links:
```
ses
session
previous
cache
img
images
forms
fg
fg-cgi
stnote
snimg
```
  
  
# Epic LPP and FDI records

  https://sites.google.com/site/yunwang/work-notes?offset=20
  
