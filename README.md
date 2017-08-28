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
