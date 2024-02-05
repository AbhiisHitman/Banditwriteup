# Banditwriteup
#Level 0
"Using SSH to log into a remote machine and execute commands on that machine"
ssh bandit0@bandit.labs.overthewire.org -p 2220

#Level0-Level1
Read contents of readme file with "cat readme" command, displaying file contents in terminal, useful for viewing file content quickly.
cat readme
Password: NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL

#Level1-Level2
Connect to bandit's shell:
ssh bandit1@bandit.labs.overthewire.org -p 2220
Retrieve password from the file named "-":

cat ./-
Password: rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi

#Level 2 -> Level 3
SSH into bandit2:
ssh bandit2@bandit.labs.overthewire.org -p 2220
Retrieve password from "spaces in this filename" file:
cat "spaces in this filename"
Password: rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi

#Level 3 -> Level 4
SSH into bandit3:

ssh bandit3@bandit.labs.overthewire.org -p 2220
Navigate to inhere directory and read .hidden file:



cd inhere
cat .hidden
Password Obtained
aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG


#Level 4 -> Level 5
SSH into bandit4:


ssh bandit4@bandit.labs.overthewire.org -p 2220
Navigate to inhere directory:


cd inhere
Identify the file containing the password:


cat ./-file07
Password Obtained lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR

#Level 5 -> Level 6
SSH into bandit5:
ssh bandit5@bandit.labs.overthewire.org -p 2220
Navigate to inhere directory and find the file with specific size:

cd inhere
find . -type f -size 1033c
Password Obtained P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU

Level 6 -> Level 7
SSH into bandit6:


ssh bandit6@bandit.labs.overthewire.org -p 2220
Use find command to locate the file with specific ownership and size:


find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
Password Obtained z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S

Level 7 -> Level 8
SSH into bandit7:


ssh bandit7@bandit.labs.overthewire.org -p 2220
Search for the word "millionth" in the data.txt file:


grep millionth data.txt
Password Obtained TESKZC0XvTetK0S9xNwm25STk5iWrBvP

Level 8 -> Level 9
SSH into bandit8:


ssh bandit8@bandit.labs.overthewire.org -p 2220
Find the unique line in data.txt:


sort data.txt | uniq -u
Password Obtained EN632PlfYiZbn3PhVK3XOGSlNInNE00t

Level 9 -> Level 10
SSH into bandit9:
ssh bandit9@bandit.labs.overthewire.org -p 2220
Extract sequences preceded by several '=' characters from data.txt:


strings data.txt | grep -o '==*.*'
Password Obtained G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s

Level 10 -> Level 11
SSH into bandit10:


ssh bandit10@bandit.labs.overthewire.org -p 2220
Decode base64 encoded data in data.txt:


base64 -d data.txt | cat -
Password Obtained 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM

Level 11 -> Level 12
SSH into bandit11:


ssh bandit11@bandit.labs.overthewire.org -p 2220
Decode ROT13 encoded data in data.txt:


cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
Password Obtained JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv

Level 12 -> Level 13
Performing operations unsuitable for the home directory, a temporary directory named "foxy" was created within /tmp, and the data.txt file was copied into that directory.


mkdir /tmp/foxy
cp data.txt /tmp/foxy/data
cd /tmp/foxy


To examine the file's header, the following command was executed to display the header of the file, akin to that of data2.bin, alongside the hex data starting with the gzip compressed file magic number '1f 8b'.


cat data | head


To proceed, the hex data was converted into an actual file by reversing it using the xxd command:


xxd -r data c_data.gz


Subsequently, the file was decompressed using gzip:


gzip -d c_data.gz

Upon inspecting the hex data of the decompressed file, it was noted to start with '42 5a 68', which corresponds to the magic number of bzip2 compressed files. Thus, the file was renamed and decompressed:


mv c_data c_data.bz2
bzip2 -d c_data.bz2


Following this, the hex data of the decompressed file revealed the gzip compressed file magic number again. Consequently, the file was renamed and decompressed:


mv c_data c_data.gz
gzip -d c_data.gz


Further analysis indicated that the hex data of the file provided little information; however, upon plain text inspection using 'cat', strings containing 'ustar', the ISO encoding for tar compressed files, were discovered. The file was then renamed and decompressed:


mv c_data c_data.tar
tar -xf c_data.tar


A new file named data5.bin appeared in the directory, which upon examination also contained 'ustar'. It was subsequently decompressed:


tar -xf data5.bin


Following this, a new file named data6.bin emerged, with its hex data indicating it was a bzip2 compressed file. It was decompressed accordingly:


bzip2 -d data6.bin


A warning might have been issued by bzip2 regarding the output file's name, which is normal for compressed files. Upon 'cat' command execution, data6.bin.out was discovered to be a tar compressed file, which was decompressed:


tar -xf data6.bin.out


Upon checking the hex data of the newly formed file data8.bin, it was found to be a gzip compressed file. It was renamed and decompressed for the last time:


mv data8.bin data8.gz
gzip -d data8.gz


Finally, the data8 file was 'cat'ed to obtain the password. The directory and files created in /tmp were automatically deleted as they were temporary.

Password Obtained:
wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw

Level 13 -> Level 14
SSH into bandit13:

ssh bandit13@bandit.labs.overthewire.org -p 2220
Use the provided private key to SSH into bandit14:


ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
No password.

Level 14 -> Level 15
SSH into bandit14:


ssh bandit14@bandit.labs.overthewire.org -p 2220
Read the password from the bandit14 file in the /etc/bandit_pass directory:


cat /etc/bandit_pass/bandit14
Intermediate Password Obtained fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq
You can't access other files anyways.
Now submit the password to the post 30000 of localhost of the current level. You can you netcat command to connect to that port.
nc localhost 30000
Password Obtained
jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt

Level 15 -> Level 16
SSH into bandit15:


ssh bandit15@bandit.labs.overthewire.org -p 2220
Connect to port 30001 via SSL encryption:


openssl s_client -connect localhost:30001
Submit the password of the current level to obtain the password for the next level.
JQttfApK4SeyHwDlI9SXGR50qclOAil1

#Level 16 -> Level 17
Connect to the Bandit server:

ssh bandit16@bandit.labs.overthewire.org -p 2220
Scan the open ports within the range 31000-32000:

nmap localhost -p T:31000-32000
After identifying the open ports, make connections to each port using the openssl command:

openssl s_client -connect localhost:31046
openssl s_client -connect localhost:31518
openssl s_client -connect localhost:31691
openssl s_client -connect localhost:31790
openssl s_client -connect localhost:31960
Submit the password to whichever server accepts it. In return, you will receive an SSH key. Save it into a file named sshkey.private.

There is no password obtained in this level.

SSH Key Obtained:
sshkey.private

Save the SSH key received into a file and name it sshkey.private.
 use this SSH key to connect to the next level.

#level17-level18
Connect to the bandit's shell using the ssk key.

ssh -i sshkey.private bandit17@bandit.labs.overthewire.org -p 2220
You will be able to see two files, namely password.old and password.new. One of the lines in the old file have been edited and saved as new file. We can find the changed line using the following command.

diff password.old password.new
The new line appended is the password.

Password Obtained
hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg
















