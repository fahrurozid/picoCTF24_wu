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

In this challenge, we are tasked with modifying all the time-related data of a photo to obtain the flag.

The first step is to download the image file to your Kali Linux or Ubuntu terminal using the following command:
`wget https://artifacts.picoctf.net/c_mimas/91/original.jpg`

Inspect the metadata of the photo by running exiftool command to view all available data `exiftool original.jpg`.
This will display all the metadata of the photo, but we will focus on the time-related data and ignore the rest.

<img width="440" alt="exif1" src="https://github.com/user-attachments/assets/86e3cdf8-a940-4677-9ccc-5eb4458029f0">

After attempting to modify all the requested metadata, you’ll notice that one piece of data remains unaltered. That data is the `TimeStamp`, which cannot be edited using exiftool.

<img width="459" alt="time" src="https://github.com/user-attachments/assets/4a3ef80e-f7f3-4419-81e6-dd4509d0fc02">

This is where the challenge gets interesting. We have to find a way to change the `TimeStamp` data in the photo.
So what we do next? run the `strings` command to inspect the contents of the image file. `strings original.jpg`

<img width="185" alt="exif4" src="https://github.com/user-attachments/assets/9196396c-4d00-4faf-960a-ee081bb842d4">

You will quickly notice a suspicious piece of data labeled `Image_UTC_Data1700513181420`. This is a timestamp, but in milliseconds format. When converted using an online converter, it reveals the date 2023:11:20 15:46:21.420–05:00.

Now we know the issue. To solve this, use a hex editing tool called ghex. Install it using the command `sudo apt install ghex`, then launch it and open the image file you want to edit. change the `TimeStamp` value `2023:11:20 15:46:21.420–05:00` to `1970:01:01 00:00:00`.

<img width="540" alt="ghex" src="https://github.com/user-attachments/assets/b7952ced-10ee-45f6-a741-6ad08127fe37">

Once you’ve finished modifying the data, run the appropriate command to verify whether the changes were successful.
Submit your modified picture `nc -w 2 mimas.picoctf.net 55709 < original_modified.jpg`.
Check your modified picture `nc mimas.picoctf.net 65250`



<img width="379" alt="exif5" src="https://github.com/user-attachments/assets/1c8dfc0f-6177-431b-ac57-994aad755564">

And voilà! We’ve successfully solved the challenge and obtained the flag.
