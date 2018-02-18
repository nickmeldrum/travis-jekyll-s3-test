﻿### The problem

We had a problem with our GIS Application. We use a 3rd party component to display our layers of maps and shapes etc. 
as an image for the browser. So we can show some pretty WMS layers underneath, we opt for a transparent PNG for our own 
layers. We want the user to be able to right-click and "save-as" this image so they can save it locally 
and play with it in whatever way they want. (Ignoring the WMS layers for now - no one's really using them yet anyway.
 We think they kind of suck for various other reasons anyway.)

So this all works in Firefox and Chrome just fine: Right-click on the image and you can save it as a .png.

Do this in Internet Explorer (tested on version 6 and 7) 
and we only get to save it as a .bmp (with the ominous "untitled" as the filename.) The problem with this is that
 annoyingly it has also assumed that our transparent sections are black instead of white which makes the image totally unusable.

(tl/dr: IE 6 and 7 (probably 8 too) only lets you save our image as .bmp instead of the original .png when right-clicking it.)

### The research

A quick google brings up these 2 KB articles: 
"[Internet Explorer Saves Images As Bitmaps (.bmp Files)](http://support.microsoft.com/kb/810978)" 
and "[Internet Explorer does not save graphics files in the proper format](http://support.microsoft.com/?kbid=260650)".
Both KB articles are talking about the same problem, but with a slightly different "view". 
 The 1st article suggests the workaround is to ensure that

 a) your cache on disk isn't full and then
 b) that any downloaded objects aren't corrupt. (no idea why b) has an effect.)

The 2nd articles suggests to clear your temporary internet files or ensure that do not save encrypted pages to disk"
 isn't checked if you are using SSL.

So whats really going on?

Well this blog post shone the light I needed:
 [http://blogs.msdn.com/jeffdav/archive/2003/12/08/53607.aspx](http://blogs.msdn.com/jeffdav/archive/2003/12/08/53607.aspx)
(He's obviously an MS IE Developer)

It turns out that the MSHTML rending engine (Trident) stores internally all images as BMPs.
 It will of course cache images to disk in their correct format. This explains why those KB articles focus on 
ensuring your cache is working correctly. If the image has been cached to disk, whatever code runs when you right-click
 and "save as" in IE can pull it from disk and use the correct image type. If it isn't in the cache it has to pull it from
MSHTML itself (ie. the in-memory representation of the web page) and it therefore only has it as a bmp.
But I ensure my cache is working fine - and still I only get a bmp as an option.

How come?

### The solution

I run [Fiddler](http://www.fiddlertool.com/) and notice that our 3rd party control puts in the HTTP Response Header:

> "Cache-Control: private, no-store"

Oh dammit - "no-store"?

So it's code out of our control (in the 3rd party component) that is not allowing IE to store it in it's cache on disk -
 so more code out of our control (mshtml) keeps the only version in memory and converted to a bmp.

I just **love** web programming sometimes.
