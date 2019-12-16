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

- Grep to filter: `ls | grep "sys"`

- Print contents: `cat [textfile]`

- Rename through moving: `mv aaa abbb`

- Create soft link: `ln -s /home/afolder /home/f/Folder`

- Change file permission:

  * `chmod g+x file` ---> [u=owner/g=group/o=other] [+-] [r=read/w=write/x=execute]

  * `chmod 705 file` ---> (eg. 0=---, 1=--x, ..., 7=rwx)

- Change owner: `chown [user]:[group] file`

- File info:  (ls -l) 	`-rw-rw-r-- 1  [user] [usergroup] [1024] [Sep 26 18:48] [file.name]`

   The first '-' indicates file type:  '-'=file, 'd'=dir, 'l'=link

- `pwd`: Print current directory path.

- apt: `apt-get install` ...

  * `apt-cache search` ...

  * `apt-cache show [package name]` (detail info)
   
  * `apt autoremove` (remove useless packages)
   
  * `apt-get update` (refresh updatable list)
   
  * `apt-get upgrade` (install update)

  * `add-apt-repository ppa:webupd8team/java` (add package source)

- `dpkg`: `-i` (install)

    * `-l` (list)

    * `-r` (remove)

    * `-p` (also purge config)

- `sudo passwd root` (change root account's password)

- `mount -t ntfs /dev/sda1 /mnt/winOS/ -o "umask=022"`

  * `umount /dev/sda1`

- `sudo -k`: Reset credential, require password to use sudo again.

- `rsync -av ~/Desktop/ ~/backup/fold1/` (A tool more powerful than cp)

  * `--exclude={"a/\*","auto\*","a/.gitignore"}`

- `systemd-analyze (time / blame / critical-chain)`

  * `systemctl (status / disable / stop)`

- System info:

  * `uname -a`: Show system info.
    
  * `inxi`: Show lots of system info (`-S` for distro/DE version)
    
  * ls /usr/bin/\*session  (Find out which DE has been installed)

- du -h /home/david: Show file's size. (can filter with grep ^[0-9]*G)

- ip addr show (the number following inet is IP)

- iotop:  View disk usage of every process.

- nmcli dev wifi: List available Wifi APs.

  * nmcli dev wifi connect [iTaiwan] password [0123456789]

- lshw: List hardware info.

- lscpu: Show cpu architecture info.

- date -d @[seconds since epoch]: convert "seconds since epoch" to readable date.

- head -n x ./myfile: Print the first x line of file/stdin (if file not provided).

- User:

  * who:  Show current user.

  * pkill -u [username]:  Logout a user.
    
  * adduser [name] --home /home/name --shell /bin/bash

- Groups:

  * groups [user]:  Show a user's groups

  * usermod -a -G [group] [user]:  Add user to a group.
	
  * gpasswd -d [user] [group]:  Remove user from a group.

- Mount eCryptfs: sudo mount -t ecryptfs [.Private] [/mnt/point] (`su` are needed sometimes)

- wmctrl -k on: Minimize all windows. (off=switch back)
