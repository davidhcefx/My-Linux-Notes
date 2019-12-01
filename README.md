# My_Linux_Note
My learning note while exploring Linux (Ubuntu XFCE)

## System Tips

1. To execute a file:  ./file

2. To create a Desktop/Launcher shortcut:  Just create a .desktop file.

3. Use TAB for auto-complete in Terminal. (Won't forget names anymore!)

4. Install RAR to unpack a .rar file.

5. System Freeze:  Try `Ctrl-Alt-F1` for accessing the terminal.

6. SysRq: `Alt` + `SysRq` + "REISUB"  ("busier")

    | | |
    |--- | --- |
    | R: exit Raw mode (X window) | E: terminate all |
    | I: force terminate | S: Sync disk |
    | U: umount disk | B: reboot |	
    | F: call oom_kill (kill one) | |

7. htop:  A handy tool for System Monitor.

8. Rapid System Simulation:  qemu-system-x86_64 [iso file]

9. Wanna list RecycleBin according to deletion time? -> Go to ~/.local/share/Trash/files, and then `stat -c "%z - %n" * | sort -t'-'`.

10. Ubuntu 16+ DO NOT run startup scripts from /etc/rcX.d anymore; Use the crontab @reboot method instead. (But do remember that root's crontab cannot read unencrypted user data)

11. Sticky bit: ------t Only owner can remove, even it is mod 777 (eg. /tmp)

12. SetUID: Do not support Scripts; Executables are also not supported under /tmp, /home. (which are mounted as nosuid)

13. Systemctl's `is-enable` command can check for "generated scripts".

14. Calling grep multiple time is faster than parsing with a single While-loop. (big file)

15. MessageOfTheDay (The tty greetings) is under /etc/update-motd.d/.

16. Locate: A utility for reverse-mapping filenames to paths. However, it will scan the whole system everyday (updatedb.mlocate), so remember to turn it off if not needed.

17. Secure boot: Not all modules are signed, hence the error message: XX kernel module not found or loaded.

## Commands

1. Grep to filter:  ls | grep "sys"

2. Print the contents:  cat [textfile]

3. Rename:  mv aaa abbb   (renaming by moving)

4. Create soft link:  ln -s /home/afolder /home/f/Folder

5. Change permission:

    a. chmod g+x file ...............> [u=owner/ g=group/ o=other], [+-], [r=read/ w=write/ x=execute]

    b. chmod 705 file ...............> (eg. 0=---, 1=--x, ..., 7=rwx)

6. Change owner:  chown [user]:[group] file

7. File info:  (ls -l) 	`-rw-rw-r-- 1  [user] [usergroup] [1024] [Sep 26 18:48] [file.name]`

   The first '-' indicates file type:  '-'=file, 'd'=dir, 'l'=link

8. Print Working Directory:  pwd (current cd)

9. apt:  apt-get install ...

   apt-cache search ...

   apt-cache show [package name]   (detail info)
   
   apt autoremove  (remove useless packages)
   
   apt-get update  (refresh update list)
   
   apt-get upgrade (install update)

   add-apt-repository ppa:webupd8team/java (package source)

10. dpkg: -i  (install)

    -l  (list)

    -r  (remove)

    -p  (remove entry also)

11. sudo passwd root   (change root account's password)

12. mount -t ntfs /dev/sda1 /mnt/winOS/

    umount /dev/sda1

13. sudo -k:  Reset credential, need password to use sudo again

14. rsync -av /home/david/Desktop/ /home/david/backup/   (A tool more powerful than cp)(Support incremental)

15. systemd-analyze  (time / blame / critical-chain)

    systemctl  (status / disable / stop)

16. uname -a:  Show all system info

17. du -h /home/david:  Show file's size and usage (can filter with ^[0-9]*G)

18. ip addr show   (number following inet is IP)

19. iotop:  View disk usage of every process

20. nmcli dev wifi:  List available Wifi AP

    nmcli dev wifi connect [iTaiwan] password [0123456789]

21. lshw:  List hardware info

22. light-locker-command -l:  Switch user (without logout)

23. head -n x ./myfile:  Print the first x line of file/stdin(if file not provided)

24. User:

    who:  Show current user

    pkill -u [username]:  Logout an user

25. Groups:

	groups [user]:  Show user's groups

    usermod -a -G [group] [user]:  Add user to a group
	
    gpasswd -d [user] [group]:  Remove user from a group

26. eCryptfs:  sudo mount -t ecryptfs [.Private] [/mnt/point]

27. wmctrl -k on:  Show desktop (off=switch back)
