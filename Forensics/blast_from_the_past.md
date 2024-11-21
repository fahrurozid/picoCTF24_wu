## Overview :

Category: **Forensics**

Level: **Medium**

Description:

The judge for these pictures is a real fan of antiques. Can you age this photo to the specifications?
Set the timestamps on this picture to 1970:01:01 00:00:00.001+00:00 with as much precision as possible for each timestamp. 
In this example, +00:00 is a timezone adjustment. Any timezone is acceptable as long as the time is equivalent. 
As an example, this timestamp is acceptable as well: 1969:12:31 19:00:00.001-05:00. 
For timestamps without a timezone adjustment, put them in GMT time (+00:00). The checker program provides the timestamp needed for each.
Use this picture.

Submit your modified picture here:
`nc -w 2 mimas.picoctf.net 55709 < original_modified.jpg`
Check your modified picture here:
`nc mimas.picoctf.net 65250`

## Solution :
download the image file in your kali linux terminal or ubuntu using this command `wget https://artifacts.picoctf.net/c_mimas/91/original.jpg`
then rename it `cp original.jpg original_mod.jpg`

check the metadata of your image using `exiftool exiftool original_modi.jpg`
you can see that the Samsung:TimeStamp is not writeabel so it can be change or modified by exiftool
so what we do now? 
you can run the strings command to see all the string in your image `strings original_mod.jpg`

