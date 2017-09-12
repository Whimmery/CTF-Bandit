## Welcome to CTF
This is my process to solving OverTheWire Bandit Wargame Levels 0-12
### Bandit - Over The Wire

![ctf bandit1](https://user-images.githubusercontent.com/31230311/29692047-0d87b38a-88fc-11e7-9f6c-3f2a089a0254.png)
![ctf bandit2](https://user-images.githubusercontent.com/31230311/29692098-4d175c80-88fc-11e7-9d98-a8cb2a05dfd4.png)
![ctf bandit3](https://user-images.githubusercontent.com/31230311/29692125-7ce84df2-88fc-11e7-84ad-130f6426cd3f.png)


```markdown
#Level 0  - logging into bandit, using the specific port and username

ssh bandit.labs.overthewire.org -p2220 -l bandit0

#Currently bandit0 has an error where it will not accept the password on first try
#Solution to password failing is to on purpose write a wrong password 
#(I wrote "bandit()" then on second request type in the right password "bandit0"

bandit()
bandit0

#Level 1- look in commands typing ls

ls

#home directory has a readme file. to read the file type "cat readme"

cat readme

#a code is given " boJ9jbbUNNfktd78OOpsqOltutMc3MY1 ", save code for next part of level
```

![ctf bandit5](https://user-images.githubusercontent.com/31230311/29692200-d0611a2c-88fc-11e7-8124-a4317bd90973.png)
![ctf bandit6](https://user-images.githubusercontent.com/31230311/29692227-ee0e678c-88fc-11e7-8997-565fc239bf28.png)


```markdown
#Level 1

#need to log into level 1 so use the original ssh log in but change "bandit0" to "bandit1" 

ssh bandit.labs.overthewire.org -p2220 -l bandit1

#type in code given in bandit0

boJ9jbbUNNfktd78OOpsqOltutMc3MY1

#Now that we are in, lets check home directory like last time to find the next password

ls

#only a dash is showing up so lets see if we can read the dash

cat -

#cat and just a dash does not work. Lets try to find the exact file that - is holding

cat < -

#The file holds the next password which is " CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9 "
#Now we need to log into Level 2
```

![ctf bandit8](https://user-images.githubusercontent.com/31230311/29692276-2a89113a-88fd-11e7-9adc-9ad0c11f6d72.png)


```markdown
#Level 2

ssh bandit.labs.overthewire.org -p2220 -l bandit2

#Next we will use the password given to us " CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9 "

CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9

#Next we got to find the directory that holds the next password. 
#Clue is "spaces in this filename" the "cat < spaces in this filename" will not work but typing in "cat spa " 
#then pressing the Tab button will work to find this folder within folders file 
#because spaces is probably the only file that starts out with that exact name

cat spaces\ in\ this\ filename

#password gotten is " UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK "
```

![ctf bandit9](https://user-images.githubusercontent.com/31230311/29692342-79349e12-88fd-11e7-8198-a0604a37ffd2.png)


```markdown
#Level 3 

#Now we log into ssh bandit.labs.overthewire.org -p2220 -l bandit3

ssh bandit.labs.overthewire.org -p2220 -l bandit3

UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK

#Using ls can lead to finding "inhere" file, but "cat inhere" does not work in showing what is inside. 
#Need to find the hidden file. 
#we can do that by ls. then a file called inhere will show. 
#we need to go inside inhere by cd, and then ls -la to look at all the files and their names inside. 
#one file name is .hidden and we can cat .hidden

ls

cat inhere

cd inhere

ls -la

cat .hidden

#Password shows up in .hidden, password is " pIwrPrtPN36QITSp3EQaw936yaFoFgAB "
```
![ctf bandit10](https://user-images.githubusercontent.com/31230311/29692377-a42b3194-88fd-11e7-89a3-811f50218dc6.png)

![ctf bandit11](https://user-images.githubusercontent.com/31230311/29692386-b69c9714-88fd-11e7-926a-695e37c7ba0e.png)


```markdown
#Level 4

# logging into ssh bandit.labs.overthewire.org -p2220 -l bandit4

ssh bandit.labs.overthewire.org -p2220 -l bandit4

#Enter password " pIwrPrtPN36QITSp3EQaw936yaFoFgAB "

pIwrPrtPN36QITSp3EQaw936yaFoFgAB

#looks at files and find inhere

ls

#next we need to see what is inside inhere

cd inhere

ls

#a bunch of files will appear, but typing in there names will not reveal anything if using cat
#best way to look through the files is to type " ./* " to search through them, 
#doing so shows that one file is different than the others and has text

./*

#next lets use ./ with the cat and the file name to read it 

cat ./-file07

#It reveals a password inside " koReBOKuIDDepwhWk7jZC0RTdopnAYKh "
```

![ctf bandit13](https://user-images.githubusercontent.com/31230311/29692419-e4673bea-88fd-11e7-85a3-9b31e754de68.png)


```markdown
#Level 5

#Let's Log in and put the password into lvl 5

ssh bandit.labs.overthewire.org -p2220 -l bandit5

koReBOKuIDDepwhWk7jZC0RTdopnAYKh

#Lets look at whats in the directory

ls

#inhere is still present so let's cd it

cd inhere

#lets see whats inside inhere

ls

#alot of files labelled as " maybehere " but using ./* does not work. using find ./* 
#shows the files but only some have different aspects to them but we do not see what meets the requirement of this level.
#to run a specific search on the requirements of this level, 
#which is "human-readable, 1033 bytes in size, not executable," we need to run a specific search
#multiple ways to look for the right file with those properties. 
#Most of the files are readable text but only one has 1033c. 
#You can use a code to find the 1033c either by "find -size 1033" 
#or you can look up the exact properties and include cat to read that file at the end 
#using " find . -type f -size 1033c -exec cat {} \;"

find . -type f -size 1033c -exec cat {} \;

#password gathered is " DXjZPULLxYr17uwoI01bNLQbtFemEgo7 "
```

![ctf bandit14](https://user-images.githubusercontent.com/31230311/29692430-fa0ac142-88fd-11e7-9b4e-59238f143c32.png)


```markdown
#Level 6

#Lets log in and using the password

ssh bandit.labs.overthewire.org -p2220 -l bandit6

DXjZPULLxYr17uwoI01bNLQbtFemEgo7

#ls does not work at all for finding the folders
# using find / -user bandit7 does bring up some files but Permission is denied
# typing in the exact requirements " find / -user bandit7 -group bandit6 -size 33c " 
#brings up more specific areas and permission denied but one section is not denied.
#type in find / -user bandit7 -group bandit6 -size 33c again but add to the end " 2>/dev/null/" 
#which redirects back to the point after reading without showing the full out put of the other files, and " cat {} \; " 
#to show what is inside without having to type it out in a new line

find / -user bandit7 -group bandit6 -size 33c 2>/dev/null -exec cat {} \;

#The password shown is " HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs "
```

![ctf bandit15](https://user-images.githubusercontent.com/31230311/29692442-08be56ae-88fe-11e7-9aec-fc87d9c54eaa.png)


```markdown
#Level 7

#Log in and use password

ssh bandit.labs.overthewire.org -p2220 -l bandit7

HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs

#if using ls a file called data.txt appears. 

ls

#using cat data.txt led to a lare list of words and codes inside. none in order, 
#but the word "millionth" should be in the txt file and next to it the password.

cat data.txt

#use grep millionth data.txt to find the word "millionth" without manually scrolling through the txt file.

grep millionth data.txt

#password found is " cvX2JJa4CFALtqS87jk27qwqGhBM9plV "
```

![ctf bandit16](https://user-images.githubusercontent.com/31230311/29759018-2cfb014a-8b86-11e7-8935-fcf36cd4141d.png)

```markdown
#Level 8

#Log into level 8 and use the password

ssh bandit.labs.overthewire.org -p2220 -l bandit8

cvX2JJa4CFALtqS87jk27qwqGhBM9plV

#just like level 7, use the cat data.txt to see what is in the data.txt file

cat data.txt

#there is no list, just everything is a mess.
#the instructions says that there is only one line of text that occurs once
#we can use a code to find that one text line
# we can use sort data.txt | uniq -u

sort data.txt | uniq -u

#this gives us the next password
#" UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR "
```

![ctf bandit17](https://user-images.githubusercontent.com/31230311/29759021-38d8e414-8b86-11e7-9624-3b6b015a5141.png)

```markdown
#Level 9

#Log in and use password


ssh bandit.labs.overthewire.org -p2220 -l bandit9

UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR

#this file is unreadable except for some strings that have "=" in it. 
#there is a way to use strings, but I will use grep
#to use grep, you will need to use "-a" which can read text files
#so the overall code would be " grep -a == data.txt "

grep -a == data.txt

#the password shows up a couple of times using "="
#but only one that shows a line of text that could be readable
# " truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk "
```

![ctf bandit17 2](https://user-images.githubusercontent.com/31230311/29759134-f4ac08c4-8b86-11e7-84a8-e3faef4faadc.png)

```markdown
#Level 10

#Log in and put in the password


ssh bandit.labs.overthewire.org -p2220 -l bandit10

truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk


#Using cat data.txt you will get a long code which is something encoded

cat data.txt

#The encode will be 
# " VGhlIHBhc3N3b3JkIGlzIElGdWt3S0dzRlc4TU9xM0lSRnFyeEUxaHhUTkViVVBSCg== "
#The instructions say that this encode uses base64 which is a form of encryption
#We need to decode the encryption using " base64 -d data.txt "

base64 -d data.txt

#It worked! The code decrypts to " IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR "
```

![ctf bandit18](https://user-images.githubusercontent.com/31230311/29759028-43cf69d8-8b86-11e7-9833-907bdc50818a.png)

```markdown
#Level 11

#Log in and use the password

ssh bandit.labs.overthewire.org -p2220 -l bandit11

IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR

#This requires a little bit of shifting letters in encryption
#we have to shift the letters over by 13
#best way to figure this out is ROT13 decoder
#I used rot13.com to figure out the cat data.txt it gave

cat data.txt

#code is " Gur cnffjbeq vf 5Gr8L4qetPEsPk8htqjhRK8XSP6x2RHh "
#rot13.com says that decoded it is
#" The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu "
```

![ctf bandit19](https://user-images.githubusercontent.com/31230311/29759035-4ece8724-8b86-11e7-8951-66b0c6ddb0f9.png)

```markdown
#Level 12

#log into the level and put the password in

ssh bandit.labs.overthewire.org -p2220 -l bandit12

5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu

#cat data.txt is used to read the file and it shows many compressed files

cat data.txt

#the clues say we need to create a directory under /tmp and use mkdir
#first I want to start a reverse file and put it into a bin file
#I am naming the bin file, honeybee.bin though it can be called anything
#this file can be used repeatedly as a source to revert the data.txt file
#honeybee.bin will now serve as anything relating to data.txt info now

xxd -r data.txt honeybee.bin

#next we will use file to also work with honeybee.bin 
#to find out what compression method was used on data.txt

file honeybee.bin

#we now find out gzip is how data.txt/honeybee.bin was compressed into a hexdump
#we now need to find a way to decompress a gzip file
#this method will use zcat and bcat to decompress
#zcat will start off compressing and now we will
#set up a way for " file - " to be linked to read honeybee.bin
#as we start compressing and decompressing the multiple compressions
#originally done to data.txt/honeybee.bin's hexdump
#using " | " to keep linking more outputs for bzcat decompressions

zcat honeybee.bin | file -

#the output says bzip2 so we must now add bzcat to the extension list
#to decompress


zcat honeybee.bin | bzcat | file -

#the output says gzip again which means that we must use zcat again
#because the user compressed the original file with gzip again at this point

zcat honeybee.bin | bzcat | zcat | file -

#The output gives us a tar extension of the file locations compression
#for multiple files that are more than 2 to be stored for extraction.
#we will use tar and whatever other extensions zcat gives
#so we can continue to decompress
#we are going to put x0 for the number of times tar has been outputted
#since we only see tar once, we will extract x0

zcat honeybee.bin | bzcat | zcat | tar xO | file -

#we see tar again so add it to the chain

zcat honeybee.bin | bzcat | zcat | tar xO | tar xO | file -

#we see bzip2 again so need to add zcat to decompress

zcat honeybee.bin | bzcat | zcat | tar xO | tar xO | bzcat | tar xO | zcat | file -

# we now see something called " ASCII text "
#since we see text that must mean 
#we have reached the honeybee.bin/data.txt to a readable file
#we will now take out " | file - " so we can decompress this chaining
#and read it without
#linking anything else to the chain

zcat honeybee.bin | bzcat | zcat | tar xO | tar xO | bzcat | tar xO | zcat

# the file decompresses and reads
#The password is " 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL "
```

![ctf bandit lvl13](https://user-images.githubusercontent.com/31230311/30310122-e9bf1c58-975c-11e7-9980-b4d646004489.png)


```markdown
#Level 13

#instead of looking for a password, we need to look for the ssh key
#to log into the next next level
#to look into this level there needs to be an understanding
#of public and private keys
#as well as key based ssh logins
#so first we need to login and use the password
#then we need to see the ssh private key for this level

ssh bandit.labs.overthewire.org -p2220 -l bandit13

8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL

#now we type in the was to see the private key

cat sshkey.private

#we now see the private key which is an encryption code
#we do not need to decrypt the key, but use it to unlock the local host

ssh bandit14@localhost -i sshkey.private 

#this lets us use the local host and the private key to
#get to the bandit14 user
#but we still need the password
#the location of the password was already given to us in the instructions
#now we just need to cat it to see if the password is there

cat /etc/bandit_pass/bandit14

#there's the password " 4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e "
#now lets use the private key and bandit14's login and ssh key

ssh -i ./sskey.private bandit14@localhost

4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e

#We're in.
```

![ctf bandit lvl14](https://user-images.githubusercontent.com/31230311/30310137-f39ce430-975c-11e7-96e5-7a2ec90145ce.png)


```markdown
#Level 14

ssh bandit.labs.overthewire.org -p2220 -l bandit14

4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e

#We do not need to log in or use a password since we already logged in
#now we need to know the password for the next level
#this level is saying we need to use port 30000 for localhost
#we can netcat or nc to access it

nc localhost 30000

#we need a password which should be the same password for this lab

4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e

#we receive a password ' BfMYroe26WYalil77FoDi9qh59eK5xNr '
```


![ctf bandit lvl15](https://user-images.githubusercontent.com/31230311/30310149-fcf8b6bc-975c-11e7-9373-7c64fe19653a.png)



```markdown
#Level 15


ssh bandit.labs.overthewire.org -p2220 -l bandit15

BfMYroe26WYalil77FoDi9qh59eK5xNr


#For this level we gotta know some openssl
#using the reading material offered we can see which steps to take next
# https://www.feistyduck.com/library/openssl-cookbook/online/ch-testing-with-openssl.html
#using the connection to ssl code from the website
#we can change the code given to feistyduck's website to instead 
#the localhost similar to the last level but with 30001

openssl s_client -connect localhost 30001

#Seeing the code it will give some commands as well as saying no port definited
#lets make try again and make the command more like a port
#adding -quiet to take out alot of the output from the results

openssl s_client -connect localhost:30001 - quiet

#it will then ask for a password 
#the password is the same for logging into level

BfMYroe26WYalil77FoDi9qh59eK5xNr

#it gives password for next level cluFn7wTiGryunymYOu4RcffSxQluehd
```

![ctf bandit lvl16](https://user-images.githubusercontent.com/31230311/30310156-09a90182-975d-11e7-8a16-3a232dd66cf9.png)


```markdown
#Level 16


ssh bandit.labs.overthewire.org -p2220 -l bandit16

cluFn7wTiGryunymYOu4RcffSxQluehd


#we are now building onto what we learned the last 2 levels
#we will be using ranges to look for the password using nmap

nmap localhost -p31000-32000

#it gives us a couple of tcp ports to try
#you can manually test them till you get the right one
#or you can use a script to test them for you
#going to nmap again to narrow it down to see which has service

nmap localhost -p31000-32000 -sV

#there is 2 connections that are showing up
#let's test them

openssl s_client -connect localhost:31790 -quiet

cluFn7wTiGryunymYOu4RcffSxQluehd

#this worked and it gave a private key

-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----

#need to echo this into a tmp file to recall it for logging into next lvl

echo "-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----" > /tmp/bandit17.key


#then need to chmod 600 /tmp/bandit17.key because
#the private key is visible and it needs to be only visible for the one user

chmod 600 /tmp/bandit17.key

#now we need to log into next level 
#while using the tmp file our private key is at

ssh bandit17@localhost -i /tmp/bandit17.key 
```

![ctf bandit lvl17](https://user-images.githubusercontent.com/31230311/30310167-18e8f666-975d-11e7-8e75-eedd5175741b.png)


```markdown
#Level 17

#using the ssh code we did from previous level
#with the private key attached
#allowed us to enter the next level 
#without needing to type in another password

ls -la

#ls -la we see there is passwords.new and passwords.old
#the instructions has a new command suggestion on using diff 
#so lets try diff for both of them

diff passwords.new passwords.old 

#This gives 2 passwords
# kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
#and
# eG69HnVwO1p7cOdfhadHkPv8Vn0ChedC
#Let's test them for the next lesson to see which works

#I'm going to assume the first one worked
#because it logged in saying "Byebye !"
#but closed because bandit18 has a block on ssh logg ins
```

![ctf bandit lvl18](https://user-images.githubusercontent.com/31230311/30310178-261984c2-975d-11e7-915b-783b1c80f4e8.png)


```markdown
#Level 18


ssh bandit.labs.overthewire.org -p2220 -i bandit18

kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd


#So we can't log in the usual ssh way into level18
#We need another way to still get to readme without logging in same way

ssh bandit.labs.overthewire.org -p2220 -l bandit18 "cat readme"
#we used the same way to log in but asked it to cat readme before disconnecting
#password is ' IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x '
```

![ctf bandit lvl19](https://user-images.githubusercontent.com/31230311/30310185-2f68ff94-975d-11e7-8bc3-5d7fa335fc12.png)


```markdown
#Level 19


ssh bandit.labs.overthewire.org -p2220 -l bandit19

IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x

#ls -la will show a file called bandit20-do

ls -la

#can't use cat
#trying to use ./bandit20-do asks for an id
#so lets see what happens if we add the hint of /etc/bandit_pass

./bandit20-do cat /etc/bandit_pass

#not working so far but bandit_pass needs to aim for 19 or 20
#/etc/bandit_pass/bandit20 works 

./bandit20-do cat /etc/bandit_pass/bandit20

#we get a password for next level ' GbKksEFF4yrVs6il55v6gwY5aVje5f0j '
```

![ctf bandit lvl20](https://user-images.githubusercontent.com/31230311/30310197-3f6d1a9c-975d-11e7-84b7-d1a916477a56.png)



```markdown
#Level 20


ssh bandit.labs.overthewire.org -p2220 -l bandit20

GbKksEFF4yrVs6il55v6gwY5aVje5f0j

#when ls -la there is suconnect showing
#this would normally require 2 terminals to make it work for a
#listerner and a receiver but it will not work
#instead make a listener and receiver in same terminal

echo "GbKksEFF4yrVs6il55v6gwY5aVje5f0j" | nc -l 1234 &

./suconnect 1234

#it gives us the password ' gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr '
```

![ctf bandit lvl21](https://user-images.githubusercontent.com/31230311/30310207-4824444e-975d-11e7-84c4-0a49ec759726.png)


```markdown
#Level 21


ssh bandit.labs.overthewire.org -p2220 -l bandit21

gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr


#ls -la to take a look see

ls -la

#I got nothing to look at beside probably prevpass
#the hints suggest looking for cron.d so let's cd into it

cd /etc/cron.d/

#let's cat into it

cat cronjob_bandit22

#it gives us /usr/bin/cronjob_bandit22.sh
#let's cat that

cat /usr/bin/cronjob_bandit22.sh

#it gives us another file /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
#let's cat again

cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv

#finally it gives us a password ' Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI '
```

![ctf bandit lvl22](https://user-images.githubusercontent.com/31230311/30310214-51ee06b8-975d-11e7-8041-2277e195323c.png)


```markdown
#Level 22


ssh bandit.labs.overthewire.org -p2220 -l bandit22

Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI

#following last lab, cd into cron.d and cat

cd /etc/cron.d/

#lets ls -la to see what's here

ls -la

#I see a folder for cronjob_bandit23
#let's cat it

cat cronjob_bandit23

#cat gave us a user link to follow
#let's cat it too!

cat /usr/bin/cronjob_bandit23.sh

#its gives us some instructions to echo copy and how to type it up
#on the line
# ( echo I am user $(whoami) | md5sum | cut -d ' ' -f 1 )
#edit whoami to 'bandit23'

echo I am user bandit23 | md5sum | cut -d ' ' -f 1

#it gave us a password ' 8ca319486bfbbc3663ea0fbe81326349 ' 
#we should use it for the tmp/mytarget it was suggesting 
#lets cat that tmp file

cat /tmp/8ca319486bfbbc3663ea0fbe81326349

#we got a password ' jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n '
#lets see if we can use it for the next level
```

![ctf bandit lvl23](https://user-images.githubusercontent.com/31230311/30310220-5b74b128-975d-11e7-81c4-ff6720e8ad5f.png)


```markdown
#Level 23


ssh bandit.labs.overthewire.org -p2220 -l bandit23

jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n

#if we ls we do not have anything out of the norm when first logging in
#let's see if what we did last level can help start us out
#we should see if we can cd into cron.d

cd /etc/cron.d/

#now we can ls -la and see there is a cronjob_bandit24
#let's try to cat it

cat cronjob_bandit24

cat /usr/bin/cronjob_bandit24.sh

#it gave us an echo saying this
# " echo "Executing and deleting all scripts in /var/spool/$myname:"
#and also gave a script
#lets see if we can make a tmp file and use the /var/spool/#myname

mkdir /tmp/noclosie


#cd into file and lets try to vim

cd /tmp/noclosie

vim derp.sh

#we are going to make a cat for the password to show up in the script
#when we run it later because the script earlier is going to close before
#the password shows, so this is our storage

cat /etc/bandit_pass/bandit24 >> /tmp/herpaderp/pass

#need to chmod 777 to make file readable and writeable
chmod 777 derp.sh

#copying the password to the file
cp derp.sh /var/spool/bandit24

#we will need to ls to get the file to read run and show in the 'pass' file
ls

ls

#we see the pass file, lets cat it

cat pass

#password shows up ' UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ '
```


![ctf bandit lvl24](https://user-images.githubusercontent.com/31230311/30310225-683e6aca-975d-11e7-9cc5-b401c8ab8bb0.png)



```markdown
#Level 24

ssh bandit.labs.overthewire.org -p2220 -l bandit24

UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ

#nc the local host 30002 and see what it says

nc localhost 30002

#"I am the pincode checker for user bandit25. 
#Please enter the password for user bandit24 
#and the secret pincode on a single line, separated by a space."

#we already have the password
#we need to brute force to get that pincode
#going to make a vim file then use a script

vim basher.sh

#!/bin/bash

pass="UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ"
for i in {1000..10000}
do {
if
    echo $pass $i| nc localhost 30002 | grep Wrong > /dev/null
then
    echo $i
else
    echo $pass $i| nc localhost 30002
    exit
fi
}
done

#now let's run the script

./basher.sh

#lets add chmod +x to make the script executable

chmod +x basher.sh

#Zzzzzzzzzzz I'll get back to you on this

#Not too long, probably 30ish mins wait.
#the pin stopped at ' 2476 '

#This is what the results say

#I am the pincode checker for user bandit25. 
#Please enter the password for user bandit24 
#and the secret pincode on a single line, separated by a space.
#Correct!
#The password of user bandit25 is uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG

Exiting.


# So the password is ' uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG '
```

![ctf bandit lvl25](https://user-images.githubusercontent.com/31230311/30310235-73eedcc4-975d-11e7-8b66-9d9754148d65.png)



```markdown
#Level 25


ssh bandit.labs.overthewire.org -p2220 -l bandit25

uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG

#if we ls or ls -la we will see a sshkey saying "bandit26.sshkey "
#let's use it to log in. Weeeee

ssh -i ./bandit26.sshkey bandit26@bandit.labs.overthewire.org -p2220

#When to log in, it automatically logs you out. Fun times.
#maybe we can just cat it before kicking us out
#when we are kicked out, we are sent back to user bandit25
#lets cat /etc/pssqd | grep bandit26

cat /etc/passwd | grep bandit26

#it will show a file saying /usr/bin/showtext
#let's cat it

cat /usr/bin/showtext

#it says it wants to show more text
#we can manually shrink the size of the terminal to as small as we can get it
#then log in using the we tried earlier

ssh -i ./bandit26.sshkey bandit26@bandit.labs.overthewire.org -p2220

#it will now let us in but we need to make a vim
#press v

v

#takes us into vim shell type in


#type :r (to run console) and then /etc/bandit_pass/bandit26 to get the level 26 password

:r /etc/bandit_pass/bandit26

#and there is our password ' 5czgV9L3Xx8JPOyRbXh6lQbmIOWvPT6Z '
#that was crazy
```


![ctf bandit lvl26](https://user-images.githubusercontent.com/31230311/30310239-7cda5cd2-975d-11e7-9b66-b967b8ff4c79.png)




```markdown
#Level 26 - 27


#now let's log into bandit 27 with the password
#heh. there is no lvl 27
#but if you stick around in bandit26 and type :shell
#you will eventually find the real bandit26 insides and there is a readme
#the read me congratulates you and says

#Congratulations on solving the last level of this game!

#At this moment, there are no more levels to play in this game. However, we #are constantly working
#on new levels and will most likely expand this game with more levels soon.
#Keep an eye out for an announcement on our usual communication channels!
#In the meantime, you could play some of our other wargames.

#If you have an idea for an awesome new level, please let us know!

#That's it! We are finished!

#A final not on bandit26
#if you have the password and the ssh, AND shrink the terminal size
#you can easily log in with 
#' ssh -i ./bandit26.sshkey bandit26@bandit.labs.overthewire.org -p2220 '
# pw: 5czgV9L3Xx8JPOyRbXh6lQbmIOWvPT6Z
#and not have to do anything extra to get easier access to the vim
#after pressing " v "
#they may fix this in the future but this is the easiest way
#to access bandit26
```
