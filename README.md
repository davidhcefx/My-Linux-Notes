# My_Linux_Note
My learning note while exploring Linux, Ubuntu and Xubuntu.

- [System Tips](#system-tips)
- [Commands](#commands)


## System Tips

1. To execute a file: `./file`

2. To create a Desktop/Launcher shortcut: Just create a `.desktop` file.

  * Beware that `%k` auto-includes `\"\"` (not documented clearly)

3. Use `TAB` for auto-complete in Terminal. (Won't forget names anymore!)

4. Install `rar` to unpack a `.rar` file.

5. System Freeze: Try `Ctrl-Alt-F1` for accessing the terminal.

6. SysRq: `Alt` + `SysRq` + "REISUB"  ("busier")

    | | |
    |--- | --- |
    | R: exit Raw mode (X window) | E: terminate all |
    | I: force terminate | S: Sync disk |
    | U: umount disk | B: reboot |	
    | F: call oom_kill (kill one) | |

7. `htop`: A colorful yet handy system resource monitor.

8. Rapid system simulation: `qemu-system-x86_64 [iso file]`

9. Wanna list RecycleBin according to deletion time? -> Go to `~/.local/share/Trash/files`, and then `stat -c "%z - %n" * | sort -t'-'`.

10. Ubuntu 16+ DO NOT run startup scripts from `/etc/rcX.d` anymore; Use the crontab `@reboot` method instead. (But do remember that root's crontab cannot read encrypted user data)

11. Crontab can be dumped and loaded: `crontab -l > dump; crontab dump`

  * The format of `/etc/crontab` is different than `crontab -e`.

12. Sticky bit: `------t` Only owner can remove, even it is mod `777` (eg. /tmp)

13. SetUID: Do not support Scripts; Executables are also not supported under `/tm`p, `/home`. (which are mounted as `nosuid`)

14. Systemctl's `is-enable` command can check for "generated scripts".

15. Calling grep multiple time is faster than parsing with a single While-loop. (big file)

16. MessageOfTheDay (The tty greetings) is under `/etc/update-motd.d/`.

17. `Locate`: A utility for reverse-mapping filenames to paths. However, it will scan the whole system everyday (`updatedb.mlocate`), so remember to turn it off if not needed.

18. Secure boot: Not all modules are signed, hence the error message: XX kernel module not found or loaded.

19. '-' is nothing special; it is just that programs such as `cat` view it as *stdin*.

20. Disable alias temporarily: 1) `command [name]`, 2) `'[name]'`, 3) `\[name]`.

21. Analyze core dumps: 1) `ulimit -c unlimited`, 2) After crash, `gdb [program] core`.

  * Can also be viewed with `readelf` or `objdump -s`, eg. *note0* section:
    ```
    OFFSET  VALUES (SIZE)
    34      pid, ppid, pgrd, sid   (DWORD)
    44      usertime, systime, cum_usertime, cum_systime (0x10)
    84      r15, r14, r13, r12     (QWORD)
    a4      bp, bx, r11, r10       (QWORD)
    c4      r9, r8, ax, cx         (QWORD)
    e4      dx, si, di, orig_ax    (QWORD)
    104     ip, cs, flags, sp      (QWORD)
    124     ss, fsbase, gsbase, ds (QWORD)
    144     es, fs, gs             (QWORD)
    ```

  * Cygwin: `export CYGWIN="$CYGWIN error_start=dumper -d %1 %2"`

22. Color is just CSI sequences, while programs detect the destination themselves (eg. ls --color=auto)

23. ptrace：only child relationship or setup PTRACE_TRACEME flag can a process been traced (`/proc/sys/kernel/yama/ptrace_scope`)


## Commands

- Read the manual: `man [something](.SECTION_NUMBER)`

  * `info [somthing]` can also be helpful.

- Grep to filter: `ls | grep "sys"`

  * `^[a-z]`: Starting / `$`: Ending / `.` Any / `?` Optional

- Print contents: `cat [textfile]`

- Rename through moving: `mv aaa abbb`

- Create soft link: `ln -s /home/afolder /home/f/Folder`

- Change file permission:

  * `chmod g+x file` ---> ['u'=owner/'g'=group/'o'=other] [+-] ['r'=read/'w'=write/'x'=execute]

  * `chmod 705 file` ---> (eg. '0'=---, '1'=--x, ..., '7'=rwx)

- Change owner: `chown [user]:[group] file`

- File info (`ls -l`): `-rw-rw-r-- 1  [user] [usergroup] [1024] [Sep 26 18:48] [file.name]`

  * The first '-' indicates file type: '-'=file, 'd'=dir, 'l'=link

- `pwd`: Print current directory path.

- apt: `apt-get install` ...

  * `apt-cache search` ...

  * `apt-cache show [package name]` (detail info)
 
  * `apt autoremove` (remove useless packages)
 
  * `apt-get update` (refresh updatable list)
 
  * `apt-get upgrade` (install update)

  * `add-apt-repository ppa:webupd8team/java` (add package source)

  * `--reinstall`

- `dpkg`: `-i` (install)

  * `-l` (list packages)

  * `-r` (remove)

  * `-p` (also purge config)

  * `dpkg-reconfigure`

- `sudo passwd root` (change root account's password)

- `mount -t ntfs /dev/sda1 /mnt/winOS/ -o "umask=022"`

  * `umount /dev/sda1`

- `sudo -k`: Reset credential, require password to use sudo again.

- `rsync -av ~/Desktop/ ~/backup/fold1/` (A tool more powerful than cp)

  * `--exclude={"a/*","auto*","a/.gitignore"}`

- `systemd-analyze (time / blame / critical-chain)`

  * `systemctl (status / disable / stop)`

- System info:

  * `uname -a`: Show system info.

  * `inxi`: Show lots of system info (`-S` for distro/DE version)

  * `ls /usr/bin/*session`  (Find out which DE has been installed)

- `du -h /home/david`: Show file's size. (can filter with `grep ^[0-9]*G`)

  * `df -h`: Show disk usage.

- `ip link`: List network interfaces (NIC). Check if there is "UP" inside <>.

  * `ip addr add [ip] broadcast + dev [interface]`: Add a static ip.

  * `ip route add default via [gateway ip] dev [interface]`: Add a default router.

  * `ifconfig eth0:0 [addr]`: Create a virtual interface.

- `iotop`:  View disk usage of every process.

- `nmcli dev wifi`: List available Wifi APs.

  * `nmcli dev wifi connect [iTaiwan] password [0123456789]`

- `lshw`: List hardware info.

- `lscpu`: Show cpu architecture info.

- `date -d @[seconds since epoch]`: convert "seconds since epoch" to readable date.

- `head -n x ./myfile`: Print the first x line of file/stdin (if file not provided).

- User:

  * `who`: Show current user.

  * `pkill -u [username]`: Logout a user.

  * `adduser [name] --home /home/name --shell /bin/bash`

- Groups:

  * `groups [user]`:  Show a user's groups

  * `usermod -a -G [group] [user]`:  Add user to a group.
	
  * `gpasswd -d [user] [group]`:  Remove user from a group.

- Mount eCryptfs: `sudo mount -t ecryptfs [.Private] [/mnt/point]` (`su` are needed sometimes)

- `wmctrl -k on`: Minimize all windows. (`off`=switch back)

- `time [command]`: Record command's execution time.
  * Get output:  `bash -c "time [command]" 2>&1`

- `xdotool`: Can emulate key presses and mouse clicks.

- `stat`: Show file modification time, size, links, type and permission.

  * `file`: Show file type.

- `xxd`: Hex dump (`-b` for binary dump)

- Message box:

  * `zenity --question --window-icon="question" --title="title" --text="some text"`

  * `notify-send -t 4000 "some message"`

- `sed`:
  * Substitution: `'4,7s/RegEx/Replace/Options'` (line 4~7)
    * Deliminator can be other than `/`, eg. `|` `:` `_`.
    * Use `\(foo\)` to remember and `\1` `\2` `\3` to recall.
    * `&` = The matching part only.
  * Options:
    * `g` = Replace all.
    * `2` = Perform on the 2nd occurence.
    * `i` = Case isensitive
    * `p` = Print matched line.
    * `d` = Delete matched line.
  * Find: `sed -n '/RegEx/p'`  (`-n` = disable echoing)
    * or `/RegEx/{lots;of;commands}`
  * Print After xxx: `0,/xxx/d;p` (GNU-only)
    * Before xxx: `0,/xxx/p`
    * It means, pretend all lines were matched (so would be deleted) until finding xxx.
  * Regex: `a*`  `a\+`  `a\?`  `\(a\|b\)`  `a\{N,M\}`  (<- N~M matches)
    * Extended (-E): `a+`  `a?`  `(a|b)`  `a{N,M}`
    * Charset: `\s` (space), `\d` (digit), `\l` (lower), `\u` (upper), `\w` (word) and `\S` (^space)
    * Regex (eg. `[0-9]*`) tries to match the longest first occurence.
  * Multiple scripts (expression): `-e 'script1' -e 'script2'`.
  * `x`: Swap pattern space with hold space. (pattern space: the matching line)
  * Escaping the replace string: `sed -e 's/[\/&]/\\&/g'`
  * Beware of shell expansion within double quotes `""`: `$`, ``` and `\\`.

- `$!`: Holds the last background process' pid.

- `find . -name [basename]` (wildcards supported)

  * Options: `-type f -size 100c -mtime -3 -maxdepth 5`

  * `find . -regex [.*full/path/regex]`

- `lsof`: find out which process opened a file.

- Vim editor:

  * `/` (search), `/\%xa9` (search hex)

  * `:d30` (delete 30 lines)

  * `ga` (show current char)

- `cut -d " " -f2`:  Print second column, seperated by a single space.

- `awk '{print $2}'`: Print second column, seperated by whitespaces.

  * `awk -v perm="-rwxr-xr-x" '$1 == perm { $1=""; print $0; system(id) }'`

- `history -c; history -r`: Clear current bash history in memory.

- `strace`: Trace all syscall of a program.

- `sudo rm -rf --no-preserve-root / &>/dev/null` (don't try it :D)

- |   | Set | Unset | Show
  | --- | --- | --- | ---
  | Shell variables   | `var=[value]`        | `unset var`     | `set`
  | Environ variables | `export var=[value]` | `export -n var` | `printenv`

  * If a variable is already in Environ, the first method would also change it.

- `trap "echo "I have been interrupted"; exit 0" SIGINT`

    * Ignore signal: `""` ; Restore to default: `-`

    * `Ctrl-c` will send SIGINT to all foreground processes (inner one handle first)

    * Avoid calling `exit 0` directly; Write `trap - SIGINT; kill -2 $$` instead.

        - For Bash uses [Wait-and-Cooperative-Exit](https://www.cons.org/cracauer/sigint.html), which will depend on how its child has terminated.

- `kill -SIGINT [process_id]`: Send signals to processes.

- `timeout [duration] [command]`: Run a command with a time limit.

- `lslogins -u`: View each user's login time, number of process etc.
