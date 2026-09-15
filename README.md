# Why you need to add timestamps to your history log

The history log in Linux is a always gathered in a forensic situation, but it is just a list of commands that is run on the system. To give this log a big increase in value you need to add timestamps to the log.<br>
This will give a time context to the commands, and will make it usable for the forensic team when they try to assemble a timeline of events.

# Restrictions
There is a restriction for adding timestamp to the history log, it will not at timestamps to previously commands in the history.<br>
So it's important that this is done when a Linux system is created.<br>
Add it to you hardening or pre-flight procedures so that it always is configured before any user starts working on the device.<br><br>

# Recomended format
From a forensics view, the best practice for date format would be year.month.day, while time format would be hour:minute:seconds<br>
The year.month.day format is the only format that gives right sorting without the need to do something with the format first.<br>
As date and time is affected by time zones and time is the most important element of a log, not only for forensics but for any situation where you need to look at logs.<br>
UTC is the universal time we work with when it comes to logs, but not all systems are set up to log in UTC, they log in local time, this is why I recommend to add time zone to the time format along with the aberration from UTC so that there is no question about what the difference from UTC really is.

# The code and how to implement it
In order to do this for every user on the linux system you need to add a bash script to the /etc/profile.d/ folder. <br>
I have choosen to name this script file history_timestamp.sh <br>
You can copy the history_timestamp.sh file from this site or you can write your own. <br>
The file contains only one line of text. <br>

export HISTTIMEFORMAT="%Y.%m.%d %H:%M:%S %Z UTC%z "

Make sure that the trailing space within the doubble quotes are kept if you type it in yourself, this is to give one blank character between the timestamp and the command in the log. <br>
And make sure the the file is executable with the sudo chmod +x /etc/profile.d/history_timestamp.sh command

# Verifying the effect
Run the command source /etc/profile.d/history_timestamp.sh command or log of and back on the system. <br>
Run a few commands like traversing directories, listing content, etc.<br>
Run the history command<br>
The history log should now show timestamps on the commands run in the verification test. If you have used this system before doing this, you will see the older commands in the list, but without a timestamp.
