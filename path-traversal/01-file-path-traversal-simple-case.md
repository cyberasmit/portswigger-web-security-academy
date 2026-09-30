# Path traversal: file path traversal, simple case

Platform: PortSwigger Academy | Level: Apprentice | Solved: 30 Sep 2026

## 1. Summary

Path traversal is also known as directory traversal. These vulnerabilities enable an attacker to read arbitrary files on the server that is running an application
A website often takes a filename from the address bar and reads that file from a folder on its server. Picture an image link like this:

https://shop.example/loadImage?filename=218.png

The server thinks: "Take 218.png from the images folder, e.g. /var/www/images/, and send it back." The bug appears when the server trusts the filename completely.

../ means "go up one folder". So if you send this instead:

filename=../../../etc/passwd

the server builds /var/www/images/../../../etc/passwd. Each ../ climbs out of the images folder, and the path ends up at /etc/passwd, a system file the site was never meant to show. That's why it's called path traversal: you traverse (walk) out of the intended folder.



## 2. How I found it

For a linux based website which is widely used we can directly get access to the file hierarchy if the website is not protected properly
i.e. filename=../../../etc/passwd

then as per the given lab instruction we can access the files through the images the website loads so,
we have to open the image in a new tab i.e. here we get "https://0a74009e0414f8ec8129700d00ad004a.web-security-academy.net/image?filename=5.jpg"

here this part "/image?filename=5.jpg" loads the image from the file
and also it gives us access to the image files which is all we need

if the server had responded with "Error 404" or "500" that means the attack have failed and if it responds with a broken image which means the lab has been solved.

## 3. Payload

The "5.jpg" is replaced with the path traversal prompt which is "https://0a74009e0414f8ec8129700d00ad004a.web-security-academy.net/image?filename=../../../etc/passwd"

## 4. Why it works

The app takes the payload which is "../../../etc/passwd" from the URL and adds it to the folder images. When I sent "https://0a74009e0414f8ec8129700d00ad004a.web-security-academy.net/image?filename=../../../etc/passwd", it built the path to previous and then to them root directory which is root, and each ../ climbed one folder up until it reached the root directory. It works because the server it trusted that the server never checked where the finish path will land and it can be used by the user to get the access to the root directory.

## 5. How to fix it

The server should resolve the final path and check that it still starts with /var/www/images/. My payload ended at /etc/passwd, which is outside that folder, so it would have been refused.
