# S3 File List Page #

## Demo ##

You can see this code in action here: 
[http://www.provensecuritysolutions.com/ciphershare/](http://www.provensecuritysolutions.com/ciphershare/)


## The Problem ##

This mini-project was born when I moved [a site](http://www.provensecuritysolutions.com) from standard GoDaddy hosting to Amazon S3's static site hosting. The site has a couple of directories of downloads that it had been directly browsable using `.htaccess` permissions. But that ability was lost with S3.

When looking for a solution to this problem, [I found that it's possible](https://aws.amazon.com/code/Amazon-S3/1713) if you're accessing access the bucket as a bucket-domain (`www.example.com.s3.amazonaws.com`); but cross-domain restrictions prevent that from working if you're using the bucket as a website (`www.example.com`, CNAME'd to something like `www.example.com.s3-website-us-east-1.amazonaws.com`). (The solution to this problem would be much easier and cleaner if AWS enabled/provided [the Access-Control-Allow-Origin header](https://forums.aws.amazon.com/thread.jspa?threadID=34281&start=125&tstart=0).)

After much cross-domain failure I hit on the idea of using an `iframe` that is loaded directly from the bucket, so it's in the same domain as the S3 REST call we ultimately want to do.

## A Solution ##

In this project you'll find two files: `index.html` and `s3_file_list_iframe.html`. The former loads the latter into an `iframe`. Because the `iframe` source is from the same domain as the 

When `index.html` is loaded in a browser, the user will be shown an expandable tree of all directories and files located under the current directory (and its subdirectories). 

## Usage ##

`index.html` should be renamed to whatever you've configured the "Index Document" to be in your S3 website bucket. 

Then copy the files into the directory that you'd like to provide a listing for. (And make sure the permissions on the files are set correctly -- i.e., make them publicly readable.)

## Compatibility ##

I've tested on Windows with Chrome, Firefox, and IE9.

## Shortcomings ##

- JavaScript is required. There's just no way around it. So no graceful degradation.

- It would have been nice to use HTTPS when accessing the bucket directly, but there's a cert mismatch with www.example.com.s3.amazonaws.com, so no dice.

- It would be good if `index.html` could get its own filename rather than using "index.html" explicitly when there's no filename in the location URL (i.e., when the "Index Document" is being hit). I couldn't figure out how to discover the implicit filename. So if you're using something other than "index.html" for your index filename, you should probably edit the `?ignore=` part of the `iframe src`.

## License ##

Licensed under the [MIT license](http://www.opensource.org/licenses/mit-license.php).

> Copyright (c) 2012 Adam Pritchard
> 
> Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
> 
> The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
> 
> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
