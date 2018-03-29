# This quick tutorial can be used to verify the integrety of a file that you have downloaded from the web before installing it on your computer. 

## Why is this important?
* Let's say I want to install the Anaconda package on my Macbook so that I can do some scientific computing. How do I know that the file I downloaded from the internet is the original file from the Anaconda group that has been untampered? What if someone altered the package and put a key-logging program within this software? You would never know without some method to verify the integrety of the original download package.


## The SHA-256 Checksum
* This technique applies a cryptographic hash function to the original file and publishes the result online. In my example, I have downloaded the Anaconda3-5.1.0-MacOSX-x86_64.pkg package from [Anaconda's website](https://docs.anaconda.com/anaconda/install/mac-os#macos-graphical-install). You can see it in my downloads folder:
```
Downloads$ ls
Anaconda3-5.1.0-MacOSX-x86_64.pkg
``` 

## Apply the checksum
* To apply the checksum, we need to locate the checksum Hash provided by Anaconda. For my edition, the checksums are shown [here](https://docs.anaconda.com/anaconda/install/hashes/Anaconda3-5.1.0-MacOSX-x86_64.pkg-hash). 
	* Hashes for Anaconda3-5.1.0-MacOSX-x86_64.pkg
* They provide the following checksum for me to verify:
	* The sha256 checksum: d6bf6309ccafa84314d85ca7421fddc16057ac2d824d698a213ccd597e896897
* Now, apply the checksum function in the terminal and verify the signature.
```
Downloads$ ls
Anaconda3-5.1.0-MacOSX-x86_64.pkg
Downloads$ shasum -a 256 Anaconda3-5.1.0-MacOSX-x86_64.pkg 
d6bf6309ccafa84314d85ca7421fddc16057ac2d824d698a213ccd597e896897  Anaconda3-5.1.0-MacOSX-x86_64.pkg
```

* If it worked out, you should see an exact match to the checksum provided online (d6bf...6897) 
* I hope that helps!
