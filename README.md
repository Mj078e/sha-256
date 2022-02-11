# sha-256
#with sha-256 some numbers in csx file, find the number
[passwords.csv](https://github.com/Mj078e/sha-256/files/8047036/passwords.csv)

import hashlib
import csv


num = list()
idd = list()
names = list()

# from 0000 to 9999 Produces and dumps them into a list
for numbers in range(10000):
    number = "{}".format(numbers).zfill(4)
    num.append(number)

# The numbers in the list of numbers are turned into sha-256 and thrown into another list
code = [hashlib.sha256(i.encode()).hexdigest() for i in num]


# Open the file and separate the members of the list and put each member in a separate list
with open('passwords.csv') as f:
    ffile = csv.reader(f)
    for line in ffile:
        name = line[0].replace(' ', '')
        names.append(name)
        for id in line[1:]:
            a = id.replace(' ', '')
            idd.append(a)


# num = list numbers 0000 to 9999
# code = list hash 0000 to 9999
# idd = list hash passwords 
# names = list names in file password


# all_code  = keys:code , value:num
# ip = keys:names , value:idd
all_code = dict(zip(code, num))
ip = dict(zip(idd, names))


for key in all_code:
    if key in ip:
        print(ip[key] + ':' + all_code[key] + '///' + key)
