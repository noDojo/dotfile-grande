<!----------------------------------------------------------
                        _//
                        _//             _//
_// _//     _//         _//   _//             _//
 _//  _// _//  _//  _// _// _//  _//    _// _//  _//
 _//  _//_//    _//_/   _//_//    _//   _//_//    _//
 _//  _// _//  _// _/   _// _//  _//    _// _//  _//
_///  _//   _//     _// _//   _//       _//   _//
                                     _///
------------------------------------------------------------>

<!----------------------------------------------------------
    from: https://github.com/dypsilon/unix-tricks
------------------------------------------------------------>

I have marked with a * those which I think are absolutely essential
Items for each section are sorted by oldest to newest. Come back soon for more!

BASH
* In bash, 'ctrl-r' searches your command history as you type
- Input from the commandline as if it were a file by replacing
  'command < file.in' with 'command <<< "some input text"'
- '^' is a sed-like operator to replace chars from last command
  'ls docs; ^docs^web^' is equal to 'ls web'. The second argument can be empty.
* '!!' expands to the last typed command. Useful for root commands:
  'cat /etc/...' [permission denied] 'sudo !!'
* '!!:n' selects the nth argument of the last command, and '!$' the last arg
  'ls file1 file2 file3; cat !!:1-2' shows all files and cats only 1 and 2
- 'ESC-.' fetches the last parameter of the previous command
* Related, include 'shopt -s histverify histreedit' on your .bashrc to
  double-check all expansions before submitting a command
- 'nohup ./long_script &' to leave stuff in background even if you logout
- 'cd -' change to the previous directory you were working on
- 'ctrl-x ctrl-e' opens an editor to work with long or complex command lines
* Use traps for cleaning up bash scripts on exit
  http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_12_02.html
* 'shopt -s cdspell' automatically fixes your 'cd folder' spelling mistakes
* Add 'set editing-mode vi' in your ~/.inputrc to use the vi keybindings
  for bash and all readline-enabled applications (python, mysql, etc)
- Aggregate history of all terminals in the same .history. On your .bashrc:
      shopt -s histappend
      export HISTSIZE=100000
      export HISTFILESIZE=100000
      export HISTCONTROL=ignoredups:erasedups
      export PROMPT_COMMAND="history -a;history -c;history -r;$PROMPT_COMMAND"
- Pressed 'Ctrl-s' by accident and the terminal is frozen? Unfreeze: 'Ctrl-Q'



PSEUDO ALIASES FOR COMMONLY USED LONG COMMANDS
- function lt() { ls -ltrsa "$@" | tail; }
- function psgrep() { ps axuf | grep -v grep | grep "$@" -i --color=auto; }
- function fname() { find . -iname "*$@*"; }
- function remove_lines_from() { grep -F -x -v -f $2 $1; }
  removes lines from $1 if they appear in $2
- alias pp="ps axuf | pager"
- alias sum="xargs | tr ' ' '+' | bc" ## Usage: echo 1 2 3 | sum
- function mcd() { mkdir $1 && cd $1; }


VIM
- ':set spell' activates vim spellchecker. Use ']s' and '[s' to move between
  mistakes, 'zg' adds to the dictionary, 'z=' suggests correctly spelled words
- check my .vimrc https://github.com/cfenollosa/dotfiles/blob/master/.vimrc


TOOLS
* 'htop' instead of 'top'
- 'ranger' is a nice console file manager for vi fans
- Use 'apt-file' to see which package provides that file you're missing
- 'dict' is a commandline dictionary
- Learn to use 'find' and 'locate' to look for files
- Compile your own version of 'screen' from the git sources. Most versions
  have a slow scrolling on a vertical split or even no vertical split at all.
  Alternatively, use 'tmux', though it is not as ubiquitous as 'screen'.
* 'trash-cli' sends files to the trash instead of deleting them forever.
  Be very careful with 'rm' or maybe make a wrapper to avoid deleting '*' by
  accident (e.g. you want to type 'rm tmp*' but type 'rm tmp *')
- 'file' gives information about a file, as image dimensions or text encoding
- 'sort -u' to check for duplicate lines
- 'echo start_backup.sh | at midnight' starts a command at the specified time
- Pipe any command over 'column -t' to nicely align the columns
* Google 'magic sysrq' to bring a Linux machine back from the dead
- 'diff --side-by-side fileA.txt fileB.txt | pager' to see a nice diff
* 'j.py' https://github.com/rupa/j2 remembers your most used folders and is an
  incredible substitute to browse directories by name instead of 'cd'
- 'dropbox_uploader.sh' lets you upload by commandline via Dropbox's API
  without the official client https://github.com/andreafabrizi/Dropbox-Uploader
- learn to use 'pushd' to save time navigating folders (j.py is better though)
- if you liked the 'psgrep' alias, check 'pgrep' as it is far more powerful
* never run 'chmod o+x * -R', capitalize the X to avoid executable files. If
  you want _only_ executable folders: 'find . -type d -exec chmod g+x {} \;'
- 'xargs' gets its input from a pipe and runs some command for each argument
* run jobs in parallel easily: 'ls *.png | parallel -j4 convert {} {.}.jpg'
- grep has a '-c' switch that counts occurences. Don't pipe grep to 'wc -l'.
- 'man hier' explains the filesystem folders for new users
- 'tree' instead of 'ls -R'
* Recover corrupt zip files: First, make copies and **ALWAYS WORK ON A COPY**
    First: 'zip -F  corrupt_copy1.zip --out recover1.zip'
    Then:  'zip -FF corrupt_copy2.zip --out recover2.zip'
    Last:  'ditto -x -k corrupt_copy3.zip --out out_folder/'
  Merge the contents of the two recovered zipfiles and the out_folder. You
  will be able to recover most of the data.
* Use GNU datamash for basic numerical, textual and statistical operations
  on text files: 'seq 10 | datamash sum 1 mean 1'


NETWORKING
- Don't know where to start? SMB is usually better than NFS for newbies.
  If really you know what you are doing, then NFS is the way to go.
* If you use 'sshfs_mount' and suffer from disconnects, use
  '-o reconnect,workaround=truncate:rename'
- 'python -m SimpleHTTPServer 8080' or 'python3 -mhttp.server localhost 8080'
  shares all the files in the current folder over HTTP.
* 'ssh -R 12345:localhost:22 -N server.com' forwards server.com's port 12345
  to your local ssh port, even if you machine is behind a firewall/NAT.
  'ssh localhost -p 12345' from server.com will get you in your machine.
* Read on 'ssh-agent' to strenghten your ssh connections using private keys,
  while avoiding typing passwords every time you ssh.
- 'socat TCP4-LISTEN:1234,fork TCP4:192.168.1.1:22' forwards your port
  1234 to another machine's port 22. Very useful for quick NAT redirection.
- Some tools to monitor network connections and bandwith:
  'lsof -i' monitors network connections in real time
  'iftop' shows bandwith usage per *connection*
  'nethogs' shows the bandwith usage per *process*
* Use this trick on .ssh/config to directly access 'host2' which is on a private
  network, and must be accessed by ssh-ing into 'host1' first
  Host host2
      ProxyCommand ssh -T host1 'nc %h %p'
  	  HostName host2
* Pipe a compressed file over ssh to avoid creating large temporary .tgz files
  'tar cz folder/ | ssh server "tar xz"' or even better, use 'rsync'
* ssmtp can use a Gmail account as SMTP and send emails from the command line.
  'echo "Hello, User!" | mail user@domain.com' ## Thanks to Adam Ziaja.
  Configure your /etc/ssmtp/ssmtp.conf:
      root=***E-MAIL***
      mailhub=smtp.gmail.com:587
      rewriteDomain=
      hostname=smtp.gmail.com:587
      UseSTARTTLS=YES
      UseTLS=YES
      AuthUser=***E-MAIL***
      AuthPass=***PASSWORD***
      AuthMethod=LOGIN
      FromLineOverride=YES