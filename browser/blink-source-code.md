# Finding the Blink source code

### tl;dr https://chromium.googlesource.com/chromium/src/+log/master/third_party/WebKit

The actively developed version of the Blink source code is found in the [Chromium source tree under "third_party/WebKit"](https://chromium.googlesource.com/chromium/src/+log/master/third_party/WebKit).

----

## Backstory

Try finding the link to the Blink source code on the Blink home page: https://www.chromium.org/blink. It appears there are links to everything but their source code.

<kbd>
<a href="https://cloud.githubusercontent.com/assets/43438/24178736/f83a2e6c-0ee5-11e7-969f-caef42f23633.png" target="_blank"><img src="https://cloud.githubusercontent.com/assets/43438/24178736/f83a2e6c-0ee5-11e7-969f-caef42f23633.png" alt="image" style="max-width:100%;"></a>
</kbd>
<br />

If you look hard enough, you may come across the link to the "codebase" hidden in the paragraph of text describing "Committing and reviewing code": https://chromium.googlesource.com/chromium/blink

However, this leads to a [codebase which was last updated over a year ago](https://chromium.googlesource.com/chromium/blink):

<kbd>
<a href="https://cloud.githubusercontent.com/assets/43438/24178569/e11fd11a-0ee4-11e7-8d8e-1ac2d42d56a5.png" target="_blank"><img src="https://cloud.githubusercontent.com/assets/43438/24178569/e11fd11a-0ee4-11e7-8d8e-1ac2d42d56a5.png" alt="image" style="max-width:100%;"></a>
</kbd>
<br />

Browsing this repo you may also discover a [blink-public](https://chromium.googlesource.com/chromium/blink-public) repo, but this too appears to be in disuse.

Searching the web [uncovers](https://github.com/ChromiumWebApps/blink) [many](https://github.com/yoavweiss/Blink) incorrect and [out-of-date answers](http://stackoverflow.com/questions/30647109/chrome-project-where-is-blink-engine-source-code/30647214#30647214) e.g.

<kbd>
<a href="https://cloud.githubusercontent.com/assets/43438/24178924/0f6e747a-0ee7-11e7-813f-31785617f0b5.png" target="_blank"><img src="https://cloud.githubusercontent.com/assets/43438/24178924/0f6e747a-0ee7-11e7-813f-31785617f0b5.png" alt="image" style="max-width:100%;"></a>
</kbd>
<br />

## Discovery of Correct URL

I finally discovered the correct location by scanning [chromium commit logs](https://chromium.googlesource.com/chromium/src/+log/master/) for a [recent commit referencing Blink](https://chromium.googlesource.com/chromium/src/+/782364b2af9f1c3c7f0a39d5dd9fa1df34cdfb09).

Blink's source now lives under "third_party/WebKit" in the Chromium repository, and was [merged a long time ago](https://groups.google.com/a/chromium.org/forum/#!topic/chromium-discuss/zIW8QyZAYlE).

https://chromium.googlesource.com/chromium/src/+log/master/third_party/WebKit

<kbd>
<a href="https://cloud.githubusercontent.com/assets/43438/24178548/c13c33ca-0ee4-11e7-9046-fbea72a53a51.png" target="_blank"><img src="https://cloud.githubusercontent.com/assets/43438/24178548/c13c33ca-0ee4-11e7-9046-fbea72a53a51.png" alt="image" style="max-width:100%;"></a>
</kbd>
<br />

Get your shit together Blink, it shouldn't be this hard to find a link to the source code. 
