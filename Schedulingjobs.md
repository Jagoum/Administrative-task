# <font color="red"> <center> Presentation On Administrative  Task </font>
## <center> Scheduling Jobs and Tasks

> ___General Objectives___ 

<font size="3">
By the end of this session, you will learn the following

- How to schedul cron jobs with cron , at , batch and systemd.

- The difference between user crontabs and system crontabs

- How to edit crontabs and how to configure the `/etc/crontab` file.

-  Some time specifications used in crontab job scheduling 

- Some   cron tab variables

- How to create system crons and user crons 

-  How to configure access to cron

- How to use `systemd` to manage crons and other alternatives to `at`.
- Overview or key points to note

# <font color="orande"> <center> Introduction  </font>
As a system admistrator schelduling task is a very important task as you will not always have time to manually monitor some activities.
 
 > 1. <font color="pink"> Cron jobs </font>
 
 Cron is daemon run at the background and wakes up every minute to  see which jobs or tasks are avialable.
 
 Anacron is a facility or program that is used to schedule jobs is good for systems that can be powered off. And they can only be edited by root users.

> 2. <font color="pink"> Differences between user cron and system cron </font>

One of the main difference between user cron and system cron is the file where they are stored eg

- user cron is stored in `/etc/spool/cron`

- system cron is stored in `/etc/crontab` file and in the `/etc/cron.d/`  directory

In scheduling cron jobs, some of the following special characters can be used

| <font color="blue"> Sysmbol   |<font color="green"> Description|<font color="red"> Examples|
|-----------|------------|-------------|
|*|This  refers to any possile value| * * * * *  `command`|
|,|This can be used to represent a list of values|* 1,2,3,4 * * * `command`|
|-|This can be used to specify a range of possible values|1-30 * * 1-20 0-6  `command`|
|/|This can be used to specify step values ie how oftem it should repeat|*/30 * * * * `command`|

> 3.  <font color="pink"> To add a cron job you can edit the crontab file </font>
```sh
vim /etc/crontab
```
or
```sh
crontab -e
```
In most linux distros we have we have some special file that can be used to schedule cron josbs.
Here are some special files used  to  schedule cron jobs
<body bgcolor="grey">

| <font color="blue"> File | <font color="green"> Function|
|-----|-----|
|`/etc/cron.d/`|It is a directory that contains anacron facilities|
|`/etc/cron.daily/`|This will exercute every script that is place  in it  every day at  12 am|
|`/etc/cron.hourly/`|This directory will exercute every file or script placed in it every hour|
|`/etc/cron.monthly/`|This directory will exercute every task of script place in it monthly ie the 1st of every month at midnight|
|`/etc/cron.weekly/`|Every task placed in this directory  will be exercuted every week ie on sunday at 12 am|

</body>
4. <font color="pink"> Some special time specifications </font><br>
As a system administator I love using this one alot to schedule my jobs

| <font color="blue"> Time specifications| <font color="green"> Functions|
|-----|-----|
|@hourly|It exercutes a job every hour|
|@daily|It exercutes a jpb every day|
|@weekly|It exercutes a job every week|
|@monthly|It exercutes a task every month|
|@yearly|It exercutes a command monthly|
5. <font color="pink">Now let's look at some cron variables</font><br>
The table below summarises the variables used in crons with some examples 

|Variable|Description|
|-----|-----|
|PATH|It is used to precise or give the absolute path to you task|
|SHELL|It is used to indicate which shell will be used to exercute the task|
|MAILTO|It is used specify the address where that should be message when the task is done|
HOME|It is used to specify the home where the code should be saved|

Hmm all this is just theoritical now lets do some practice
> Examples

Lets say I want to run my hello.sh script minute after two days.

Note:

- By default the mail will be send to the user who added the cron jobs
- To remonve a schedule cron job use `cron -r`
- To see scheduled cron jobs use `cron -l` 
- To check your mail you can
- To specify the name of the user whose crontabs need to be edited use `crontab -u username`

```
cat /var/spool/mail/username 
```
> Solution

``` 
crontab -e  
- add the  lines below
*  *  */2  *   *  /home/username/directory/hello.sh
```
You can also add system crons in /etc/cron.daily/ directory.


> 6. scheduling cron jobs with `at ` command

`at` is a  one time job scheduling command that is used to schedule jobs that should occur once.

> Examples 

`at  now +minutes echo "My first at job "> file.txt`

`at teatime cat file.txt` 
 
 Teatime is  16:00 OR 4:00 pm