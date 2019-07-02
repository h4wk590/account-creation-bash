#!/bin/bash

#Author: Aidan Brown
#ITAS 181 Assignment02

#Adding the Year 1 & 2 groups.
groupadd ITASYR1
groupadd ITASYR2


#Declaring the users as year 1 or 2 as int variables.
declare -i uid=1001
declare -i uid2=2001


#Cat outputs the data from the userdata.csv file and pipes it into a translate flag
#the tr -d command translates the file to remove all "/" from it.
#The while loop uses IFS to read the file left to right.
#echos out the variables created from the IFS command

cat userdata.csv | tr -d ' /' |  while IFS=',' read  fname lname bdate data;
do


                        echo "$fname $lname $bdate $data"



#User variables set
#'propername' variable created to be used as fname + lname


fname=${fname,,}
lname=${lname,,}
fullname="${fname^}, ${lname^}"
bdate=${bdate:4:2}${bdate:2:2}${bdate:0:2}
data=${data,,}



#Creating the variables for the username

username=${fname:0:1}${lname}
password=${fname:0:1}${lname:0:1}$bday

#If the variable data(year column in csv) is = to 'year1'
#Then add the user to the ITASYR1 group with the full name
#Else add the user to the ITASYR2 group with the full name

if [ $data = 'year1' ];
then

useradd $username -g ITASYR1 -u $uid -c "$fullname"
echo $password | passwd $username --stdin
let "uid+=1"

elif [ $data = 'year2' ];
then
useradd $username -g ITASYR2 -u $uid2 -c "$fullname"
echo $password | passwd $username --stdin
let "uid2+=1"

fi

done

