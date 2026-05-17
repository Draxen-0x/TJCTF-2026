
**Description : I changed just one little thing and my racing moose won't run anymore !**

Link of Challenge : [Chall](https://tjctf-2026-infra.storage.googleapis.com/uploads/809dce67817bef879a2f573da162614fbe2a01f2b04633128e4921cf6968d627/chall)

صلي علي النبي

![[Remoose Description.png]]



### 1) Introduction

**Type of the file : data**

![[Type File.png]]


**Now I will see bytes in hex of these file**


![[Magic Bytes.png]]

**In Magic Bytes  , I see that magic bytes : `ELK`**

**I want to be `ELF` so , i will change `0x4b` to `0x46`**



**![[Space.png]]**

**The `0x00` bytes were replaced with `0x20`, which caused the binary to be unexecutable** 

**Therefore, I will restore the original values to the binary in order to make it executable again.**


**I make python script to patch the file to make file executable** 

```python
with open("chall", "rb") as f:
    raw_data = f.read()

fixed = bytearray(raw_data)

for i in range(len(fixed)):
    if fixed[i] == 0x20:
        fixed[i] = 0x00

fixed[3] = 0x46

with open("chall_fixed", "wb") as f:
    f.write(fixed)
```


**After I run the Python script**

**![[Fixed script.png]]**



### 2) Static Analysis


**I see that `Main` Function call `flag` Function**


**![[Main Function.png]]**


#### **2.1) Flag (First Part)**


**I enter to the `flag` Function** 

**I see the First part from the flag**

**First Part of the Flag : `tjctf{`**


**![[Flag Funcion.png]]**


**`sub_1030` --> `putchar('')`**

**`sub_1040` --> `printf("")`**

**like :**

**`putchar('t');**
**`putchar('j');`**
**`putchar('c');`**
**`putchar('t');`**
**`printf("f{");`**


#### **2.2) Flag (Second Part)**


**I see that `flag` Function call `flag1` Function**

**I enter to the `flag1` Function** 

**I see the Second part from the flag**

**Second Part of the Flag : `5m`**


**![[Flag1 Function.png]]**


#### **2.3) Flag (Third Part)**


**I see that `flag1` Function call `flag2` Function**

**I enter to the `flag2` Function** 

**I see the Third part from the flag**

**Third Part of the Flag : `a11_`**


**![[Flag2 Function.png]]**


#### **2.4) Flag (Fourth Part)**


**I see that `flag2` Function call `flag3` Function**

**I enter to the `flag3` Function** 

**I see the Fourth part from the flag**

**Fourth Part of the Flag : `m0`**


**![[Flag3 Function.png]]**


#### **2.5) Flag (Fifth Part)**

**I see that `flag3` Function call `flag4` Function**

**I enter to the `flag4` Function** 

**I see the Fifth part from the flag**

**Fifth Part of the Flag : `0s3}`**


**![[Flag4 Function.png]]**



### **3) Flag**

**First Part of the Flag : `tjctf{`**

**Second Part of the Flag : `5m`**

**Third Part of the Flag : `a11_`**

**Fourth Part of the Flag : `m0`**

**Fifth Part of the Flag : `0s3}`**


**Flag : `tjctf{5ma11_m00s3}`**