# Removing-Audible-DRM
Converting protected AAX to DRM free mp3 and m4a files in just a few seconds using Ubuntu


Quick tutorial on how to strip the Audible DRM from AAX files from a remote server. I did this so I would be able to broadcast my audiobooks to all members of my discord via a bot I made.

## Prerequisites

* Ubuntu
* FFMPEG
* Legit Audible membership 
* Audible Download manager (installed and verified)
* InAudible (may require iTunes audible plugin as well)

It will work with Ubuntu desktops as well, but for this case I'm using a remote server.

## Step 1 - Download the admhelper file

Append the contents of the admhelper file after this URL:

> http://cdl.audible.com/cgi-bin/aw_assemble_title_dynamic.aa?

So the final URL will look like this:

> http://cdl.audible.com/cgi-bin/aw_assemble_title_dynamic.aa?user_id=UHUIHGUIYBIUBIUGBIUBIYGBYBFIUFBUYF&cust_id=HJGYGYGYVYJHGJHKGJVJVGVJ&product_id=BK_PNIX_000930&asin=&codec=LC_64_25850_stereo&awtype=AAX&source=audible_adm&title=The King Within: Accessing the King in the Male Psyche&assemble_url=http://cds.audible.com/download&order_number=D01-031572024-9567927&size=&domain=www.audible.com&transfer_player=1&browser_type=

Now use *wget* to download the file in terminal.

>$ wget http://cdl.audible.com/cgi-bin/aw_assemble_title_dynamic.aa?user_id=UHUIHGUIYBIUBIUGBIUBIYGBYBFIUFBUYF&cust_id=HJGYGYGYVYJHGJHKGJVJVGVJ&product_id=BK_PNIX_000930&asin=&codec=LC_64_25850_stereo&awtype=AAX&source=audible_adm&title=The King Within: Accessing the King in the Male Psyche&assemble_url=http://cds.audible.com/download&order_number=D01-031572024-9567927&size=&domain=www.audible.com&transfer_player=1&browser_type=

Rename the file to something more humanly usable, eg: book.aax

## Step 2

Download and install InAudible. This is to get the 4byte decryption key. I don't know how it generates this key because I was not prompted to log in when using it. Reddit mentioned it may use the iTunes Audible plugin to generate it so in case it doesnt run, install itunes and the audible plugin and try again. 

Run the wizard and open any AAX file on your local system. If you look at the output logs, the decryption key is there. It looks like:

> 94csf312

## Step 3 - Convert

In the same directory as *book.aax*, run the following command:

>  ffmpeg -y -activation_bytes 94csf312 -i 'book.aax' -c:a copy -vn 'book.m4a'

This takes literally just mere seconds in my dedicated server. The end result is a m4a file that is DRM free. Enjoy
