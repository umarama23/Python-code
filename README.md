# Python-code
import os
import sys
cwd=os.getcwd()
(setpath,Examples)=os.path.split(cwd)
print setpath
sys.path.append(setpath)

from PyArduino import *

import struct


port=locateport()
ser = serial.Serial(port, 9600)

ser.write("\x01\x03\x15\x86\x00\x02\x39\x15")
buf=ser.read(11)
b1=b2=b3=b4=0

a1=buf[3]

if (a1<16):
    b1=1
    a1=int(a1,16)
if (b1):
    a1='0'+str(a1)


a2=buf[4]
if (a2<16):
    b2=1
    a2=int(a2,16)
if (b2):
    a2='0'+str(a2)
    a3=buf[5]
if (a3<16):
    b3=1
    a3=int(a3,16)
if (b3):
    a3='0'+str(a3)

a4=buf[6]
if (a4<16):
    b4=1
    a4=int(a4,16)
if (b4):
    a4='0'+str(a4)


a5=[a3,a4,a1,a2];
a6=''.join(a5)


print struct.unpack('!f', a6.decode('hex'))[0]
