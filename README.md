# picoCTF-hideme #
 
## Challenge ##

![image alt](https://github.com/Field2548/picoCTF-hideme/blob/c28ceba1ab9240e04a31c879be6ad4ebe67a08cd/Challenge.png)

## Solution ##

First, I downloaded the flag.png file given by the challenge. Then I took a look around to identify any clues or useful information within the image's details, using an online exiftool -> https://exif.tools. 

![image alt](https://github.com/Field2548/picoCTF-hideme/blob/1dec12788bc27bb0ea32811f36a49d83927f6b66/exiftool.png)

However, I was not able to find anything there, so I try to searched the file with a hex editor (https://hexed.it) and was able to spot something interesting there:

![image alt](https://github.com/Field2548/picoCTF-hideme/blob/678d3f25de57ed78e62b2571e7ac2ae5b4afd724/hexeditor.png)

As you may noticed, "secret/flag.png" seems to be something that will help in finding our flag. However, I was not that proficient in forensic yet so I I was unsure of its exact significance. To better understand, I googled about cryptography-particularly topics relating to file hidden in an image and came across a tool called 'Binwalk' from this website: https://ctfs.github.io/resources/topics/steganography/file-in-image/README.html

![image alt](https://github.com/Field2548/picoCTF-hideme/blob/1dec12788bc27bb0ea32811f36a49d83927f6b66/Binwalk.png)

The `binwalk` utility detected a ZIP archive appended to the original `flag.png` image file.

The ZIP archive was extracted using the command `binwalk -e`, which automatically identifies and extracts embedded files from the image.

![image alt](https://github.com/Field2548/picoCTF-hideme/blob/1dec12788bc27bb0ea32811f36a49d83927f6b66/binwalk%20-e%20result.png)

Next, I accessed the extracted ZIP file and downloaded the image from the webshell using the `sz` command.

![image alt](https://github.com/Field2548/picoCTF-hideme/blob/1dec12788bc27bb0ea32811f36a49d83927f6b66/download%20file%20to%20computer.png)

This process revealed another 'flag.png' file located at 'hideme/_flag.png.extracted/secret/flag.png'. Hurray!!! We can find our flag with an image editor, allowing us to capture and submit it.

![image alt](https://github.com/Field2548/picoCTF-hideme/blob/1dec12788bc27bb0ea32811f36a49d83927f6b66/flag-2.png)
