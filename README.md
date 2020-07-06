# terminal-cheat-sheet
Cheat sheet for common terminal (Bash) commands.  You may find that not all of these will work in your shell environment.

**Present Working Directory:**

```
pwd
```

**Using man with a native function (ex. scp) returns information regarding the function:**

```
man function
```
 
**Go to root:**

```
cd ~
```
 
**List files in directory:**

```
ls
```

**Create file:**

```
touch filename
```
 
**Delete file:**

```
rm path/file
```

**Delete directory with sub-directories and files:**

```
rm –rf path/directory
```

**Make dir:**

```
mkdir directoryname
```

**Move dir or file:**

```
mv path/to/source path/to/destination
```

**Copy dir or file:**

```
cp -R path/to/source path/to/destination
```
 
**Get into Root Mode:**

```
sudo -s
```

**Get out of Root Mode:**

```
exit
```

**Monitor file (use Ctrl+C to stop):**

```
tail -F path/to/source
```
 
**Get first line of file:**

```
head -1 <pathtofile>
```
 
**View file:**

```
cat filename
```

**“Scroll” through a file:**

```
less filename
```
 
**Compare and get difference between files or directories, the -r makes sure to compare sub-directories and content within:**

```
diff -r /path/file1 /path/file2
```

**copy remote files on capistrano to local hd:**

```
scp capistrano@appdev03:/path/dw_build.sh dw_build.sh
```
 
**Copies all files and sub-directories from external source to the currently active local directory (note the period):**

```
scp -r capistrano@appdev03:/path/to/directory .
```

**Copy single file from external source to the currently active local directory (note the period):**

```
scp capistrano@appdev03:google_trusted/cpo_gtrust_shipments_F.txt .
```

**Opens currently active directory in Finder:**

```
open .
```

**List with full date:**

```
ls --full-time (only Linux?)
ls -aoT  (all files, size, last modified)
```

**Push local files to remote area (you may need to run pwd to find out path on remote dir):**

```
scp promo-app-test.zip capistrano@appdev03:/path/to/directory/
```

**Use curl to save the contents of a webpage to a file on the desktop:**

```
curl http://www.google.com > ~/Desktop/test.html
or better, follow redirects:
curl -L --max-time 30 --location-trusted --insecure --connect-timeout 10 --request GET http://www.google.com > ~/Desktop/test.html
or silent with fail:
curl -sSL --max-time 30 --silent --location-trusted --insecure --connect-timeout 10 --request GET http://www.google.com
```

**This will look through a file (...log) for any blocks of content with “ERROR” and if found space blocks of content with two spaces and write data to a text file (newErrors.txt)**

```
grep "ERROR" -C2 errorlog.log > newErrors.txt
```

**Find all files in current directory with the extension “csv” and delete them.**

```
find . "*.csv" | rm
```

**Look for string in file:**

```
grep -n 'string' file.xml
```

**Get range of lines from a file:**

```
sed -n 2,4p somefile.txt
sed -n -e 1,2p -e 4p somefile.txt
```

**Get last 10 lines of file**

```
tail -10 somefile.txt
```

**Get files by string in directory “archive”**

```
grep -r 'myString' archive/
```

**Get files by string in current directory with line numbers**

```
grep -nr 'myString'
```

**Get files with line numbers that contain search term in all child dirs**

```
grep -HEroine 'searchstring' *
```

**Get number of lines in file:**

```
wc -l < file.csv
```

**Trim string:**

```
line=’string’;
line=${line//[$'\t\r\n ']};
echo $line;
```

**Sort:**

```
sort file1.csv > file2.csv
```

**Sort & Unique:**

```
sort file1.csv | uniq > file2.csv
```

**Remove “ (double-quote in this example could be any character):**

```
echo ‘string’ | sed -e s,\",,g
```

**Print columns 5,7,9,23 using ‘<’ as input and output delimiter (awk doesn’t respect delimiters in  “”):**

```
awk -F "<" '{ OFS = "<"}{print $5,$7,$9,$23 }' input.csv >> output.csv
```

**Remove lines that contain ‘Deleted’:**

```
grep -vwE "Deleted" input.csv > output.csv
```

**This is a handy little command line operation that creates a csv of file names in a directory:**

```
ls -lT | awk '{print "\""substr($0,index($0,$10))"\""",""\""$6" "$7", "$9"\""",""\""$5"\""}' > folderlist.csv
```

**Output program's stdout and stderr to file**
http://stackoverflow.com/questions/418896/how-to-redirect-output-to-a-file-and-stdout

```
program [arguments...] 2>&1 | tee -a outfile

or more concise:

<command> |& tee -a  <outputFile>
```

**Above the -a prevents info in the file from overwriting contents, appends to file.**
using unbuffer should help keep output properly written in "correct" order, but not all environments have unbuffer

```
unbuffer program [arguments...] 2>&1 | tee -a outfile
```

**Base 64 some file:**

```
echo "data:$(file -b --mime-type somefile);base64,$(base64 somefile)"
```

##Screen##

**If the process is running on your computer, you’ll need to change your computer’s power settings so it won’t go to sleep and thus stopping your process.**  This is especially handy when you want a single long running process to do something on a remote computer (e.g. EC2) and not have to keep a terminal session active.  However, for repeating processings you'd like to schedule look into systemd or CRON.

**Create named screen:**

```
screen -S myScreenName
```

**Detach from screen (while process is running):**

```
Ctrl + a, Ctrl + d
```

**View available screens:**

```
screen -ls
```

**Reattach to named screen:**

```
screen -d -r myScreenName
```

**Destroy detached screen:**

```
screen -X -S sessionID quit
```

**Alternatives:**
nohup sounds difficult to re-attach to and it directs stdout to nohup.log
https://stackoverflow.com/questions/26568135/keep-alive-express-process-after-close-the-terminal
https://askubuntu.com/questions/8653/how-to-keep-processes-running-after-ending-ssh-session
https://www.computerhope.com/unix/unohup.htm
https://askubuntu.com/questions/57477/bring-nohup-job-to-foreground
Tmux is another possibility, not sure if it redirects stdout


##VIM##

**Edit file**

```
vim path/to/file
```

Once open press "i" key to begin editing.  To exit press esc key, type ```:x``` to save and exit or ```:q!``` to quit without saving.

**Learn vim:**

```
vimtutor
```

**Delete all lines:**

```
:%d
```

**Your personal Vim initializations (customizations):**

```
~/.vimrc   
```

**System wide Vim initializations (customizations):**

```
/usr/local/lib/vim/vimrc (path may vary)
```


##CRON JOBS##

```
crontab -e
crontab -l
```


##SQLite3##

First create db with structure:

```
sqlite3 CSVDATA.db

create table data_all(account CHAR, date DATE, publisher CHAR, campaign_num INT);
```

**Import CSVs (after creating db structure, above)**

```
.separator '<'
.import 'filename.csv' data_all
```

**Set output as text**

```
.output unsorted-unique-urls.csv
```

**Or set output back to stdout**

```
.output stdout
```

**Then performed queries**

```
SELECT DISTINCT redirect_url from data_all WHERE (publisher COLLATE nocase = 'active' OR publisher COLLATE nocase = 'paused');

SELECT COUNT(*) from data_all WHERE (publisher COLLATE nocase = 'active' OR publisher COLLATE nocase = 'paused');

INSERT INTO data_all values(2014-02-13,’active’,’3.0’);
```


##Bash file for SQLite3##

Example of file contents for bash script that operates on SQLite3 db

```
#!/bin/bash

# Defining my database first table
STRUCTURE="CREATE TABLE data (id INTEGER PRIMARY KEY,name TEXT,value TEXT);";

# Creating an Empty db file and filling it with my structure
mkdir tmp;
echo $STRUCTURE > tmp/tmpstructure;
sqlite3 dbname.db < tmp/tmpstructure;
rm -rf tmp;

# Inserting some data into my structure
sqlite3 dbname.db "INSERT INTO data (name,value) VALUES ('MyName','MyValue')";
sqlite3 dbname.db "INSERT INTO data (name,value) VALUES ('MyOtherName','MyOtherValue')";

# Getting my data
LIST=`sqlite3 dbname.db "SELECT * FROM data WHERE 1"`;

# For each row
for ROW in $LIST; do

    # Parsing data (sqlite3 returns a pipe separated string)
    Id=`echo $ROW | awk '{split($0,a,"|"); print a[1]}'`
    Name=`echo $ROW | awk '{split($0,a,"|"); print a[2]}'`
    Value=`echo $ROW | awk '{split($0,a,"|"); print a[3]}'`

    # Printing my data
    echo 'id:' $Id  'name:' $Name  'value:' $Value;

done

# Note that using: COUNT(*) is different then COUNT(column_name)
# In the latter, nulls are filtered out
```


##Linux (commands may not work with all versions)##


**Shutdown:**

```
sudo poweroff
Or
sudo shutdown -h now
Or
systemctl poweroff
```

**Restart:**

```
sudo reboot
Or
sudo shutdown -r now
Or
systemctl reboot
```


**Log into one of 6 virtual desktop (text-only) consoles:**

```
Ctrl+Atl +F2 (or F3-F6)
```

**Switch back to GUI desktop:**

```
Ctrl-Alt-F7
```

##REFERENCES##
 
http://linux.about.com/library/cmd/blcmdl1_less.htm
http://www.go2linux.org/head-Linux-command-to-display-the-benning-of-a-file
http://www.cyberciti.biz/faq/howto-search-find-file-for-text-string/
http://stackoverflow.com/questions/6712437/find-duplicate-lines-in-a-file-and-count-how-many-time-each-line-was-duplicated
http://www.computerhope.com/unix/utail.htm
http://www.computerhope.com/unix/udiff.htm
http://linux.about.com/library/cmd/blcmdl1_diff.htm
https://www.sqlite.org/sqlite.html
http://hackgeo.com/foss/sqlite-how-to-import-csv
http://sqlite.awardspace.info/syntax/sqlitepg02.htm
http://stackoverflow.com/questions/2698108/count-columns-group-by



