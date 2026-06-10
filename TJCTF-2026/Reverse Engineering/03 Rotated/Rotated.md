
**Description : this file isn't making any sense to me. can you discover what it means?**

**Link of Challenge : [Chall](https://tjctf-2026-infra.storage.googleapis.com/uploads/d7622db106133782a0ad97832104f4a454f1eb062a324de037bbbdc708f292d2/chall)**

**صلي علي النبي** 

<img width="461" height="232" alt="Image" src="https://github.com/user-attachments/assets/03c510c3-5110-403e-a7dd-789226ef0314" />



### 1) Introduction


**Type of the file : data**

<img width="527" height="136" alt="Image" src="https://github.com/user-attachments/assets/12ba90bc-b6a0-4e4a-8457-9ccc5ff89797" />


**Now I will see bytes in hex of these file**

<img width="621" height="632" alt="Image" src="https://github.com/user-attachments/assets/4ecc67f9-438e-4cb1-8d59-0be69764abf6" />

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

<img width="342" height="66" alt="Image" src="https://github.com/user-attachments/assets/0bec9860-f987-4907-b318-e773d3f7489b" />

**I will run it** 

<img width="331" height="66" alt="Image" src="https://github.com/user-attachments/assets/c3c7ccf4-3b6b-442e-a9bb-3d68318cca16" />


**After I run python script** 

**It creates file `new_elf`**

**`new_elf` is real executable file and after I run it**

**file create bash script `script.sh`**


<img width="393" height="269" alt="Image" src="https://github.com/user-attachments/assets/415430b1-fe4c-4c39-81b8-46f6f12f5f80" />



### 2) Decrypt Flag


**`script.sh` has bash noise like :  `${@//...}`**

**The main script :**

**printf** 

**`H4sIAEDAzmkC/0tNzshXUPLJz8/OzEtXSMsvUkhUSMtJTLdXUlBWSHEvyEpxjzKPzAo0THSzzPY18jL0y7Es8XMJNfY19rJ0Tre1BQCGqZA9QQAAAA==`**


<img width="1897" height="267" alt="Image" src="https://github.com/user-attachments/assets/9f551ec0-9f32-4157-b2d7-06cfe5856524" />

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


<img width="555" height="75" alt="Image" src="https://github.com/user-attachments/assets/845f9ece-2265-40ba-9c68-f05fe6f30618" />


**I will take the flag :**

**`dGpjdGZ7YjQ1aF9kM2J1Nl9tNDU3M3J9Cg==`**

**Type of encoding : `base64`** 

 **I will decode it by Cyberchef Tool**


<img width="1333" height="811" alt="Image" src="https://github.com/user-attachments/assets/d9f31e3e-ef34-4065-8860-17357959b845" />


### 3) Flag


**Flag : `tjctf{b45h_d3bu6_m4573r}`**
