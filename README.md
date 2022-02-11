# sha-256
with sha-256 some numbers in csx file, find the number
[passwords.csv](https://github.com/Mj078e/sha-256/files/8047036/passwords.csv)

import hashlib
import csv


num = list()
idd = list()
names = list()

# az 0000 ta 9999 miad tolid mikone va to ye list mirize
for numbers in range(10000):
    number = "{}".format(numbers).zfill(4)
    num.append(number)

# adad haye toye list adad 0000 ta 9999 ro tabdil be hash mikone
code = [hashlib.sha256(i.encode()).hexdigest() for i in num]


# baz kardan list va joda kardan ozv ha va rikhtanshon to ye list
with open('passwords.csv') as f:
    ffile = csv.reader(f)
    for line in ffile:
        name = line[0].replace(' ', '')
        names.append(name)
        for id in line[1:]:
            a = id.replace(' ', '')
            idd.append(a)


# num = list adad 0000 ta 9999
# code = list hash 0000 ta 9999
# idd = list hash password ha hast
# names = list esm haye toye file password hast


# all_code  = keys:code , value:num
# ip = keys:names , value:idd
all_code = dict(zip(code, num))
ip = dict(zip(idd, names))


for key in all_code:
    if key in ip:
        print(ip[key] + ':' + all_code[key] + '///' + key)
