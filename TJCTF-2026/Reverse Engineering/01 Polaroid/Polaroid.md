
**Description : this old polaroid won't develop. it needs a password, and the password is somewhere on the film.**

**Link of Challenge : [Polaroid](https://tjctf-2026-infra.storage.googleapis.com/uploads/645d579c7c5fa2673f69b6da7acb1b04822af26d417ac7b50e08370466fe614a/polaroid)**

**صلي علي النبي**


![[Polaroid Description.png]]



### 1) Introduction


**File Format : Mach-O file** 

**Architecture : ARM 64-bit**



### 2) Static Analysis


![[Password.png]]


**This Program want password** 


**Password length : `17`**

**Password : `exposeTheNegative`**


**This Program run MacOS** 

**If you have MacOS write this command in the Terminal**

```
./polaroid exposeTheNegative
```

**but If you don't have MacOS write this python script that decrypt the data by password to create a image** 

```python
data = open('polaroid', 'rb').read()

password = b'exposeTheNegative'
const_offset = 0x720
const_size = 0x18b4
encrypted = data[const_offset:const_offset+const_size]

result = bytearray()
for i, b in enumerate(encrypted):
    result.append(b ^ password[i % len(password)])

with open('flag.png', 'wb') as f:
    f.write(result)

print("Done! flag.png created")
```

**What does this Python script do? :**

**1. Read the binary file as raw bytes**

**2. Extract the encrypted data from the `__const` section at offset `0x720` with size `0x18b4`**

**3. XOR every byte of the encrypted data with the password**

**4. Write the decrypted result as `flag.png`**


### 3) Flag


**After I run Python script , It creates `flag.png`**

![[Flag.png]]

**Flag After Rotation** 

![[Flag After Rotation.png]]


**Flag : `tjctf{develop_the_picture}`**