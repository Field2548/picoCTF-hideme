# picoCTF-hideme #
 
## Challenge ##

![image alt](https://github.com/Field2548/picoCTF-hideme/blob/c28ceba1ab9240e04a31c879be6ad4ebe67a08cd/Challenge.png)

## Solution ##

First, I downloaded the flag.png file given by the challenge. Then I took a look around to identify any clues or useful information within the image's details, using an online exiftool -> https://exif.tools. However, I was not able to find anything there, so I try to searched the file with a hex editor (https://hexed.it) and was able to spot something interesting there:




and using `strings`, there was no flag, however I did find references to a "secret" and "secret/flag.png", but nothing in the form of `picoCTF{flag}`.



The `binwalk` utility identified a zip archive appended to the original flag image file :

    $ binwalk flag.png 

    DECIMAL       HEXADECIMAL     DESCRIPTION
    --------------------------------------------------------------------------------
    0             0x0             PNG image, 512 x 504, 8-bit/color RGBA, non-interlaced
    41            0x29            Zlib compressed data, compressed
    39739         0x9B3B          Zip archive data, at least v1.0 to extract, name: secret/
    39804         0x9B7C          Zip archive data, at least v2.0 to extract, compressed size: 2997, uncompressed size: 3152, name: secret/flag.png
    43036         0xA81C          End of Zip archive, footer length: 22

The zip archive was extract using `binwalk` :

    $ binwalk -e flag.png

This yielded another `flag.png` within `hideme/_flag.png.extracted/secret/flag.png` which when viewed with an image editor and displayed the flag (actual flag value redacted for the purposes of this write up):

    picoCTF{........redacted........}
