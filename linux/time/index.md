### Linux Display Current Date and Time
```
$ date
Mon Jan 21 01:31:40 IST 2019
```

### Linux Display The Hardware Clock (RTC)
Type the following hwclock command to read the Hardware Clock and display the time on screen:
```
$ hwclock -r
```
OR
```
$ hwclock --show
$ sudo hwclock --show --verbose
```
Show it in Coordinated Universal time (UTC):
```
$ hwclock --show --utc
2019-01-21 01:30:50.608410+05:30
```

### Linux Set Date Command Example
Use the following syntax to set new data and time:
```
$ date --set="STRING"
```

For example, set new date to 2 Oct 2006 18:00:00,
type the following command as root user:
```
$ date -s "2 OCT 2006 18:00:00"
```
OR
```
$ date --set="2 OCT 2006 18:00:00"
```

You can also simplify format using following syntax:
```
$ date +%Y%m%d -s "20081128"
```
Linux Set Time Examples
To set time use the following syntax:
```
$ date +%T -s "10:13:13"
```
10: Hour (hh), 13: Minute (mm), 13: Second (ss)

Use %p locale’s equivalent of either AM or PM, enter:
```
$ date +%T%p -s "6:10:30AM"
$ date +%T%p -s "12:10:30PM"
```

### How do I set the Hardware Clock to the current System Time?
Use the following syntax:
```
$ hwclock --systohc
```
OR
```
$ hwclock -w
```

```
A note about systemd based Linux system
With systemd based system you need to use the timedatectl command to set or view the current date and time. Most modern distro such as RHEL/CentOS v.7.x+, Fedora Linux, Debian, Ubuntu, Arch Linux and other systemd based system need to the timedatectl utility. Please note that the above command should work on modern system too.

timedatectl: Display the current date and time
Type the following command:
$ timedatectl


Fig.01: Systemd Linux timedatecetl command to display the current date and time
Fig.01: Systemd Linux timedatecetl command to display the current date and time
How do I change the current date using the timedatectl command?
To change the current date, type the following command as root user:
# timedatectl set-time YYYY-MM-DD

OR
$ sudo timedatectl set-time YYYY-MM-DD

For example set the current date to 2015-12-01 (1st, Dec, 2015):
# timedatectl set-time '2015-12-01'
# timedatectl

Sample outputs:

      Local time: Tue 2015-12-01 00:00:03 EST
  Universal time: Tue 2015-12-01 05:00:03 UTC
          RTC time: Tue 2015-12-01 05:00:03
       Time zone: America/New_York (EST, -0500)
     NTP enabled: no
NTP synchronized: no
 RTC in local TZ: no
      DST active: no
 Last DST change: DST ended at
                  Sun 2015-11-01 01:59:59 EDT
                  Sun 2015-11-01 01:00:00 EST
 Next DST change: DST begins (the clock jumps one hour forward) at
                  Sun 2016-03-13 01:59:59 EST
                  Sun 2016-03-13 03:00:00 EDT
To change both the date and time, use the following syntax:
# timedatectl set-time YYYY-MM-DD HH:MM:SS

Where,

HH : An hour.
MM : A minute.
SS : A second, all typed in two-digit form.
YYYY: A four-digit year.
MM : A two-digit month.
DD: A two-digit day of the month.
For example, set the date ’23rd Nov 2015′ and time to ‘8:10:40 am’, enter:
# timedatectl set-time '2015-11-23 08:10:40'
# date

How do I set the current time only?
The syntax is:
# timedatectl set-time HH:MM:SS
# timedatectl set-time '10:42:43'
# date

Sample outputs:

Mon Nov 23 08:10:41 EST 2015
How do I set the time zone using timedatectl command?
To see list all available time zones, enter:
$ timedatectl list-timezones
$ timedatectl list-timezones | more
$ timedatectl list-timezones | grep -i asia
$ timedatectl list-timezones | grep America/New
To set the time zone to ‘Asia/Kolkata’, enter:
# timedatectl set-timezone 'Asia/Kolkata'

Verify it:
# timedatectl

      Local time: Mon 2015-11-23 08:17:04 IST
  Universal time: Mon 2015-11-23 02:47:04 UTC
        RTC time: Mon 2015-11-23 13:16:09
       Time zone: Asia/Kolkata (IST, +0530)
     NTP enabled: no
NTP synchronized: no
 RTC in local TZ: no
      DST active: n/a
How do I synchronizing the system clock with a remote server using NTP?
Simply type the following command:
# timedatectl set-ntp yes
Verify it:
$ timedatectl

Sample outputs:

      Local time: Mon 2015-11-23 08:18:49 IST
  Universal time: Mon 2015-11-23 02:48:49 UTC
        RTC time: Mon 2015-11-23 02:48:50
       Time zone: Asia/Kolkata (IST, +0530)
     NTP enabled: yes
NTP synchronized: yes
 RTC in local TZ: no
      DST active: n/a
```
Conclusion
Linux users can use date command to print or set the system date and time. 
Systemd based Linux users can use timedatectl to control the system time and date.
