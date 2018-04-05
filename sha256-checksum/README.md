# The SHA-256 Checksum: Authenticate Programs from the Web 
This quick tutorial can be used to verify the integrety of a file that you have downloaded from the web before installing it on your computer. 

## Why is this important?
Let's say I want to install a program from the web on my laptop. I'm an engineer interested in installing the Anaconda package on my Macbook so that I can do some scientific computing using Jupyter. How do I know that the file I downloaded from the internet is the original, untampered file from the Anaconda group? What if someone altered the package and put some malicious code (say, a key-logging program for instance) within this software package? We need a way to verify the authenticity of a program before installing it on our home computers and this is what the SHA-256 Checksum is used for.


## The SHA-256 Checksum
The SHA-256 algorithm is a cryptographic hash function that takes an input file (the package you want to download) and produces an output hash (the checksum) that is unique to that file. If the file is altered in anyway from it's original state, even a just a single bit, will produce a completely different hash output.  


Check it out. Let's create a simple text file and compute the checksum:


```
sha256-checksum$ echo 'This is the original file (1)' >> original.txt
sha256-checksum$ cat original.txt 
This is the original file (1)
```
Compute the checksum on this file:

```
sha256-checksum$ shasum -a 256 original.txt 
3f465258cb48959348de0e402a81b00817a7267983d6d677118426fac397c450  original.txt
```


The output hash <3f465258cb48959348de0e402a81b00817a7267983d6d677118426fac397c450> is the unique checksum for this file. Now, let's alter original.file a little and check the new checksum (I only changed the 1 to a 2, shown below).


```
sha256-checksum$ vim original.txt 
This is not the original file!

sha256-checksum$ cat original.txt 
This is not the original file!
```


But the checksum should be totaly different.

```
sha256-checksum$ shasum -a 256 original.txt 
8d14c5e71db91b6290e58efad61702595f8ba7cd94b7eca62df3848625a655af  original.txt
```


## Apply the checksum
So, let's use this in real life. In my example, I have downloaded the Anaconda3-5.1.0-MacOSX-x86_64.pkg package from [Anaconda's website](https://docs.anaconda.com/anaconda/install/mac-os#macos-graphical-install). You can see it in my downloads folder:

```
Downloads$ ls
Anaconda3-5.1.0-MacOSX-x86_64.pkg
``` 


To apply the checksum, we need to locate the checksum Hash provided by Anaconda. For my edition, the checksums are shown [here](https://docs.anaconda.com/anaconda/install/hashes/Anaconda3-5.1.0-MacOSX-x86_64.pkg-hash). 


The original programmers for this package publish the SHA-256 hash at the download website. The Hash (checksum) for my Anaconda3-5.1.0-MacOSX-x86_64.pkg is:

* The sha256 checksum:
	* d6bf6309ccafa84314d85ca7421fddc16057ac2d824d698a213ccd597e896897


Now, apply the checksum function in the terminal and verify the signature.

```
Downloads$ ls
Anaconda3-5.1.0-MacOSX-x86_64.pkg
Downloads$ shasum -a 256 Anaconda3-5.1.0-MacOSX-x86_64.pkg 
d6bf6309ccafa84314d85ca7421fddc16057ac2d824d698a213ccd597e896897  Anaconda3-5.1.0-MacOSX-x86_64.pkg
```

If it worked out, you should see an exact match to the checksum provided online: d6bf6309ccafa84314d85ca7421fddc16057ac2d824d698a213ccd597e896897


I hope you find this helpful!
