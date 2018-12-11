# captcha-cracking
Simple captcha cracking methods 

Using following simple steps you can easily convert and automatically recognize alpha-numeric captcha with high rate of success.
It may be useful for fast creation of proof-of-concept.

**Preparement:**
Install required packages
```sh
# apt install tesseract-ocr libtesseract4 imagemagick curl
```

**Step 1:**
Download image
```sh
# curl -s -o captcha.png https://example.com/captcha.png
```
<img src="captcha.png" width=500px/>

**Step 2:**
Make image black and white, monochrome using imagemagic tools.
Option
```sh
# convert captcha.png -fill black -fuzz 30% +opaque "#BAB5BB" -negate -monochrome result.png
```
<img src="result.png" width=500px/>

**Step 3:**
Run tesseract to recognize image and read out.txt with cat.
Option '-c' is used for specifying config with alfabet
```sh
# tesseract result.png out --oem 0 -c tessedit_char_whitelist=abcdefghijklmnopqrstuvwxyz0123456789; cat out.txt
Tesseract Open Source OCR Engine v4.0.0 with Leptonica
Warning: Invalid resolution 0 dpi. Using 70 instead.
Estimating resolution as 321
29c70d
```

**Additional info:**
I had to install eng.traineddata from github, because the tainedata file for tesseract from kali repo was broken
```
# rm /usr/share/tesseract-ocr/4.00/tessdata/eng.traineddata; wget https://github.com/tesseract-ocr/tessdata/raw/master/eng.traineddata -O /usr/share/tesseract-ocr/4.00/tessdata/eng.traineddata
```
Tesseract version used:
```
tesseract-ocr/kali-rolling,now 4.0.0-1+b1 amd64 [installed]
```
