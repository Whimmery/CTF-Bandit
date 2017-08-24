## Welcome to CTF
This is a CTF test page showing part of the OverTheWire wargame for Bandit
### Bandit - Over The Wire



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




```markdown
#Level 2

ssh bandit.labs.overthewire.org -p2220 -l bandit2

#Next we will use the password given to us " CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9 "

CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9

#Next we got to find the directory that holds the next password. 
#Clue is "spaces in this filename" the "cat < spaces in this filename" will not work but typing in "cat spa " 
#then tab button will work to find this folder within folder file 
#because spaces is probably the only file that starts out with that exact name

cat spaces\ in\ this\ filename

#password gotten is " UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK "
```




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
