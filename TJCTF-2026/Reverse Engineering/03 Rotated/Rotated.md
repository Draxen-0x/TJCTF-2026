
**Description : this file isn't making any sense to me. can you discover what it means?**

**Link of Challenge : [Chall](https://tjctf-2026-infra.storage.googleapis.com/uploads/d7622db106133782a0ad97832104f4a454f1eb062a324de037bbbdc708f292d2/chall)**

**صلي علي النبي** 

![[Rotated Description.png]]



### 1) Introduction


**Type of the file : data**

**![[Type of File.png]]**


**Now I will see bytes in hex of these file**

**![[Hex Bytes of File.png]]**

**so First 4 bytes :**

**`9c 62 69 63`**



**I want to change it from : ** 

**`9c 62 69 63`**
     ||
     ||
     V 
**`7f 45 4c 46`**


**to be like ELF file to execute file** 


**`9c - 7f = 1d`**
**`62 - 45 = 1d`**
**`69 - 4c = 1d`**
**`63 - 46 = 1d`**

**so I will subtract `0x1d` from all bytes of file Like : **

**Byte - `0x1d` = New_Byte**


**I write simple python script that change bytes automatically**

```python
data = open('chall', 'rb').read()
new_bytes = bytes([(b - 0x1d) % 256 for b in data])
open('new_elf', 'wb').write(new_bytes)
```

![[ELF Script.png]]

**I will run it** 

**![[Run Python Script.png]]**


**After I run python script** 

**It creates file `new_elf`**

**`new_elf` is real executable file and after I run it**

**file create bash script `script.sh`**


**![[Create Script.sh.png]]**



### 2) Decrypt Flag


**`script.sh` has bash noise like :  `${@//...}`**

**The main script :**

**printf** 

**`H4sIAEDAzmkC/0tNzshXUPLJz8/OzEtXSMsvUkhUSMtJTLdXUlBWSHEvyEpxjzKPzAo0THSzzPY18jL0y7Es8XMJNfY19rJ0Tre1BQCGqZA9QQAAAA==`**


**![[Run Script.sh.png]]**

**This is text of flag :**

**`H4sIAEDAzmkC/0tNzshXUPLJz8/OzEtXSMsvUkhUSMtJTLdXUlBWSHEvyEpxjzKPzAo0THSzzPY18jL0y7Es8XMJNfY19rJ0Tre1BQCGqZA9QQAAAA==`**

**but it compressed by `gzip` and encoded by `base64`**

**so I will decode it and after I decode it , I will decompress it by `gzip.decompress`**

**I will make these steps by python script :** 

```python
import base64, gzip

flag_enc = 'H4sIAEDAzmkC/0tNzshXUPLJz8/OzEtXSMsvUkhUSMtJTLdXUlBWSHEvyEpxjzKPzAo0THSzzPY18jL0y7Es8XMJNfY19rJ0Tre1BQCGqZA9QQAAAA=='
real_flag = gzip.decompress(base64.b64decode(flag_enc))
print(real_flag.decode())
```


**The result of script :** 


**![[Flag_dec Script.png]]**


**I will take the flag :**

**`dGpjdGZ7YjQ1aF9kM2J1Nl9tNDU3M3J9Cg==`**

**Type of encoding : `base64`** 

 **I will decode it by Cyberchef Tool**


**![[Decode Flag.png]]**


### 3) Flag


**Flag : `tjctf{b45h_d3bu6_m4573r}`**
