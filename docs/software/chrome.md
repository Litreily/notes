# Chrome

## 快捷键

|快捷键|说明|
|:---|:---|
|`F1`|打开帮助页面|
|`F3, Ctrl-F`|打开搜索框|
|`F5, Ctrl-R`|刷新当前页|
|`F6, Ctrl-L, Alt-D`|移动并选中地址栏信息|
|`F11`|切换全屏|
|`F12, Ctrl-Shift-I`|打开开发调试工具|
|`Ctrl-N`|打开新窗口|
|`Ctrl-T`|打开新标签页|
|`Ctrl-Shift-N`|在隐身模式下打开新窗口|
|`Ctrl-1 ~ Ctrl-8`|切换指定编号的标签页|
|`Ctrl-9`|切换至最后一个标签页|
|`Ctrl-Tab, Ctrl-PgDown`|切换至下一个标签页|
|`Ctrl-Shift-Tab, Ctrl-PgUp`|切换至下一个标签页|
|`Ctrl-Shift-B`|打开或关闭书签栏|
|`Ctrl-W, Ctrl-F4`|关闭当前标签页或弹出式窗口|
|`Ctrl-D`|收藏当前页|
|`Alt-Home`|打开主页|
|`Shift-ESC`|查看任务管理器|
|`Ctrl-J`|查看下载页|
|`Ctrl-H`|查看历史记录页|
|`Ctrl-P`|打印当前页|
|`Ctrl-S`|保存当前页|
|`Ctrl-U`|查看当前网页源码|
|`Ctrl-Shift-C`|打开开发工具，选择指定元素|
|`Space, PgDown`|向下翻页|
|`Shift-Space, PgUp`|向上翻页|
|`Home`|翻页至顶部|
|`End`|翻页至底部|

## 插件

### Tampermonkey

`tampermonkey`也称油猴脚本，堪称浏览器利器，通过安装各类脚本对网站进行定制，定制化功能之多，只有想不到，没有做不到。

下面记录下我使用或编写的几个脚本：

- [安装]防别人知道你在看知乎,删除知乎固定的标题

上班空闲时间刷刷知乎是常有的事，但是默认知乎标题是置顶显示的，不想让旁人看见，所以安装了以下脚本。

``` javascript
// ==UserScript==
// @name         防别人知道你在看知乎,删除知乎固定的标题
// @namespace    http://tampermonkey.net/
// @version      0.1
// @description  try to take over the world!
// @author       gagayuan
// @match        https://www.zhihu.com/*
// @grant        none
// @require    http://code.jquery.com/jquery-1.11.0.min.js
// ==/UserScript==

(function() {
    'use strict';
    $("div.PageHeader").remove();
    $("div.Sticky").remove();
    $("svg.ZhihuLogo").remove();
    $("button.Button--blue").css("background-color","#ebebeb").css("border-color","#ebebeb");
    $("button.VoteButton").css("color","#b8adad").css("background","#f6f6f6");
})();
```

- [原创]停止显示谷歌搜索下拉提示

在公司使用谷歌搜索，默认是会有下拉提示的，某些情况下如果他人在操作我的电脑，看到些与工作不符的搜索信息就不太好了，所以禁止下拉提示就很重要，但偏偏浏览器默认没有这个选项，或者说只能全局禁止。所以就有了以下脚本↓

``` javascript
// ==UserScript==
// @name         停止显示谷歌搜索下拉提示
// @namespace    http://tampermonkey.net/
// @version      0.1
// @description  try to take over the world!
// @author       www.litreily.top
// @include      https://www.google.com/*
// @include      https://cn.bing.com/*
// @grant        none
// @require      http://code.jquery.com/jquery-1.11.0.min.js
// ==/UserScript==

(function() {
    'use strict';
    // for google search
    $("div[jscontroller='tg8oTe']").remove()

    // for bing search
    // $('div#sw_as').remove()
})();
```

- [安装]网页限制解除

### Adblock Plus

`Adblock Plus`是款免费的广告拦截器，一直在用，从此告别广告，安心学习娱乐，这款插件针对每个网站进行单独设定广告拦截与否，还可以通过过滤器拦截指定元素。

### cVim

`cVim` 将网页当成一个vim编辑器，通过它可以使用`vim`的操作方式操作网页，从此告别鼠标，简直爽到爆！用了就停不下来那种！

最近更新Chrome后，`cVim`无法使用`f/F`键进行提示了，最后搜索发现该插件使用了被deprecated的API，根据下面的方法可以临时解决：

> <https://github.com/1995eaton/chromium-vim/issues/716>  
> To get `hints` working again: in `hints.js:727`, replace call to `main.createShadowRoot()` with `main.attachShadow({mode: 'open'})`

- KeyBindings

| Movement |  | Mapping name |
|:---|:---|:---|
| `j,s` | scroll down | scrollDown |
| `k,w` | scroll up | scrollUp |
| `h` | scroll left | scrollLeft |
| `l` | scroll right | scrollRight |
| `d` | scroll half-page down | scrollPageDown |
| `unmapped` | scroll full-page down | scrollFullPageDown |
| `u,e` | scroll half-page up | scrollPageUp |
| `unmapped` | scroll full-page up | scrollFullPageUp |
| `gg` | scroll to the top of the page | scrollToTop |
| `G` | scroll to the bottom of the page | scrollToBottom |
| `0` | scroll to the left of the page | scrollToLeft |
| `$` | scroll to the right of the page | scrollToRight |
| `#` | reset the scroll focus to the main page | resetScrollFocus |
| `gi` | go to first input box | goToInput |
| `gI` | go to the last focused input box by `gi` | goToLastInput |
| `zz` | center page to current search match (middle) | centerMatchH |
| `zt` | center page to current search match (top) | centerMatchT |
| `zb` | center page to current search match (bottom) | centerMatchB |
| **Link Hints** |  |  |
| `f` | open link in current tab | createHint |
| `F` | open link in new tab | createTabbedHint |
| `unmapped` | open link in new tab (active) | createActiveTabbedHint |
| `W` | open link in new window | createHintWindow |
| `A` | repeat last hint command | openLastHint |
| `q` | trigger a hover event (mouseover + mouseenter) | createHoverHint |
| `Q` | trigger a unhover event (mouseout + mouseleave) | createUnhoverHint |
| `mf` | open multiple links | createMultiHint |
| `unmapped` | edit text with external editor | createEditHint |
| `unmapped` | call a code block with the link as the first argument | createScriptHint(&lt;FUNCTION_NAME&gt;) |
| `unmapped` | opens images in a new tab | fullImageHint |
| `mr` | reverse image search multiple links | multiReverseImage |
| `my` | yank multiple links (open the list of links with P) | multiYankUrl |
| `gy` | copy URL from link to clipboard | yankUrl |
| `gr` | reverse image search (google images) | reverseImage |
| `;` | change the link hint focus |  |
| **QuickMarks** |  |  |
| `M<*>` | create quickmark <*> | addQuickMark |
| `go<*>` | open quickmark <*> in the current tab | openQuickMark |
| `gn<*>` | open quickmark <*> in a new tab | openQuickMarkTabbed |
| `gw<*>` | open quickmark <*> in a new window | openQuickMarkWindowed |
| **Miscellaneous** |  |  |
| `a` | "alias to "":tabnew google """ | :tabnew google |
| `.` | repeat the last command | repeatCommand |
| `:` | open command bar | openCommandBar |
| `/` | open search bar | openSearchBar |
| `?` | open search bar (reverse search) | openSearchBarReverse |
| `unmapped` | open link search bar (same as pressing`/?`) | openLinkSearchBar |
| `I` | search through browser history | :history |
| `<N>g%` | scroll &lt;N&gt; percent down the page | percentScroll |
| `<N>unmapped` | pass`<N>`keys through to the current page | passKeys |
| `i` | enter insert mode (escape to exit) | insertMode |
| `r` | reload the current tab | reloadTab |
| `gR` | reload the current tab + local cache | reloadTabUncached |
| `;<*>` | create mark <*> | setMark |
| `''` | go to last scroll position | lastScrollPosition |
| `<C-o>` | go to previous scroll position | previousScrollPosition |
| `<C-i>` | go to next scroll position | nextScrollPosition |
| `'<*>` | go to mark <*> | goToMark |
| `cm` | mute/unmute a tab | muteTab |
| `none` | reload all tabs | reloadAllTabs |
| `cr` | reload all tabs but current | reloadAllButCurrent |
| `zi` | zoom page in | zoomPageIn |
| `zo` | zoom page out | zoomPageOut |
| `z0` | zoom page to original size | zoomOrig |
| `z<Enter>` | toggle image zoom (same as clicking the image on image-only pages) | toggleImageZoom |
| `gd` | alias to :chrome://downloads | :chrome://downloads |
| `ge` | alias to :chrome://extensions | :chrome://extensions |
| `yy` | copy the URL of the current page to the clipboard | yankDocumentUrl |
| `yY` | copy the URL of the current frame to the clipboard | yankRootUrl |
| `ya` | copy the URLs in the current window | yankWindowUrls |
| `yh` | copy the currently matched text from find mode (if any) | yankHighlight |
| `b` | search through bookmarks | :bookmarks |
| `p` | open the clipboard selection | openPaste |
| `P` | open the clipboard selection in a new tab | openPasteTab |
| `gj` | hide the download shelf | hideDownloadsShelf |
| `gf` | cycle through iframes | nextFrame |
| `gF` | go to the root frame | rootFrame |
| `gq` | stop the current tab from loading | cancelWebRequest |
| `gQ` | stop all tabs from loading | cancelAllWebRequests |
| `gu` | go up one path in the URL | goUpUrl |
| `gU` | go to to the base URL | goToRootUrl |
| `gs` | go to the view-source:// page for the current Url | :viewsource! |
| `<C-b>` | create or toggle a bookmark for the current URL | createBookmark |
| `unmapped` | close all browser windows | quitChrome |
| `g-` | decrement the first number in the URL path (e.g`www.example.com/5`=>`www.example.com/4`) | decrementURLPath |
| `g+` | increment the first number in the URL path | incrementURLPath |
| **Tab Navigation** |  |  |
| `gt,K,R` | navigate to the next tab | nextTab |
| `gT,J,E` | navigate to the previous tab | previousTab |
| `g0,g$` | go to the first/last tab | "firstTab, lastTab" |
| `<C-S-h>,gh` | open the last URL in the current tab’s history in a new tab | openLastLinkInTab |
| `<C-S-l>,gl` | open the next URL from the current tab’s history in a new tab | openNextLinkInTab |
| `x` | close the current tab | closeTab |
| `gxT` | close the tab to the left of the current tab | closeTabLeft |
| `gxt` | close the tab to the right of the current tab | closeTabRight |
| `gx0` | close all tabs to the left of the current tab | closeTabsToLeft |
| `gx$` | close all tabs to the right of the current tab | closeTabsToRight |
| `X` | open the last closed tab | lastClosedTab |
| `t` | :tabnew | :tabnew |
| `T` | :tabnew &lt;CURRENT URL&gt; | :tabnew @% |
| `O` | :open &lt;CURRENT URL&gt; | :open @% |
| `<N>%` | switch to tab &lt;N&gt; | goToTab |
| `H,S` | go back | goBack |
| `L,D` | go forward | goForward |
| `B` | search for another active tab | :buffer |
| `<` | move current tab left | moveTabLeft |
| `>` | move current tab right | moveTabRight |
| `]]` | "click the ""next"" link on the page (see nextmatchpattern above)" | nextMatchPattern |
| `[[` | "click the ""back"" link on the page (see previousmatchpattern above)" | previousMatchPattern |
| `gp` | pin/unpin the current tab | pinTab |
| `<C-6>` | toggle the focus between the last used tabs | lastUsedTab |
| **Find Mode** |  |  |
| `n` | next search result | nextSearchResult |
| `N` | previous search result | previousSearchResult |
| `v` | enter visual/caret mode (highlight current search/selection) | toggleVisualMode |
| `V` | enter visual line mode from caret mode/currently highlighted search | toggleVisualLineMode |
| `unmapped` | clear search mode highlighting | clearSearchHighlight |
| **Visual/Caret Mode** |  |  |
| `<Esc>` | exit visual mode to caret mode/exit caret mode to normal mode |  |
| `v` | toggle between visual/caret mode |  |
| `h,j,k,l` | move the caret position/extend the visual selection |  |
| `y` | copys the current selection |  |
| `n` | select the next search result |  |
| `N` | select the previous search result |  |
| `p` | open highlighted text in current tab |  |
| `P` | open highlighted text in new tab |  |
| **Text boxes** |  |  |
| `<C-i>` | move cursor to the beginning of the line | beginningOfLine |
| `<C-e>` | move cursor to the end of the line | endOfLine |
| `<C-u>` | delete to the beginning of the line | deleteToBeginning |
| `<C-o>` | delete to the end of the line | deleteToEnd |
| `<C-y>` | delete back one word | deleteWord |
| `<C-p>` | delete forward one word | deleteForwardWord |
| `unmapped` | delete back one character | deleteChar |
| `unmapped` | delete forward one character | deleteForwardChar |
| `<C-h>` | move cursor back one word | backwardWord |
| `<C-l>` | move cursor forward one word | forwardWord |
| `<C-f>` | move cursor forward one letter | forwardChar |
| `<C-b>` | move cursor back one letter | backwardChar |
| `<C-j>` | move cursor forward one line | forwardLine |
| `<C-k>` | move cursor back one line | backwardLine |
| `unmapped` | select input text (equivalent to`<C-a>`) | selectAll |
| `unmapped` | edit with Vim in a terminal (need the`cvim_server.py`script running for this to work and the VIM_COMMAND set inside that script) | editWithVim |

- Command Mode

| Command | Description |
|:---|:---|
| :tabnew (autocomplete) | open a new tab with the typed/completed search |
| :new (autocomplete) | open a new window with the typed/completed search |
| :open (autocomplete) | open the typed/completed URL/google search |
| :history (autocomplete) | search through browser history |
| :bookmarks (autocomplete) | search through bookmarks |
| :bookmarks /&lt;folder&gt; (autocomplete) | browse bookmarks by folder/open all bookmarks from folder |
| :set (autocomplete) | temporarily change a cVim setting |
| :chrome:// (autocomplete) | open a chrome:// URL |
| :tabhistory (autocomplete) | browse the different history states of the current tab |
| :command &lt;NAME&gt; &lt;ACTION&gt; | aliases :&lt;NAME&gt; to :&lt;ACTION&gt; |
| :quit | close the current tab |
| :qall | close the current window |
| :restore (autocomplete) | restore a previously closed tab (newer versions of Chrome only) |
| :tabattach (autocomplete) | move the current tab to another open window |
| :tabdetach | move the current tab to a new window |
| :file (autocomplete) | open a local file |
| :source (autocomplete) | load a cVimrc file into memory (this will overwrite the settings in the options page if the localconfig setting had been set previously |
| :duplicate | duplicate the current tab |
| :settings | open the settings page |
| :nohlsearch | clear the highlighted text from the last search |
| :execute | execute a sequence of keys (Useful for mappings. For example, "map j :execute 2j") |
| :buffer (autocomplete) | change to a different tab |
| :mksession | create a new session from the current tabs in the active window |
| :delsession (autocomplete) | delete a saved session |
| :session (autocomplete) | open the tabs from a saved session in a new window |
| :script | run JavaScript on the current page |
| :togglepin | toggle the pin state of the current tab |
| :pintab | pin the current tab |
| :unpintab | unpin the current tab |

对于需要禁用的网站，可以在`cVim`的[配置页面](chrome-extension://ihlenndgcmojhcghmfjfneahoeklbjjh/pages/options.html)中设置黑名单，如：

``` javascript
let blacklists = ["https://www.shiyanlou.com/*"]
```

### Evernote Web Clipper

印象笔记的剪藏工具，可惜公司网络没法用

### GNOME Shell integration

`GNOME`主题优化插件，可以通过它安装各种系统小工具，天气显示、CPU info等等。

### Katalon Recorder

这个一个`Selenium`测试用的生成工具，通过捕捉用户操作生成对应的脚本，对于许多重复性的测试工作可以用它先生成测试脚本，然后通过`python`实现自动化测试

### Octotree

`Github`项目目录树，使用侧边栏树形目录显示代码结构，和浏览本地目录一样，方便快捷，非常好用，但仅支持开源项目，私有项目不能使用。

### Proxy SwitchyOmega

科学上网必备！隐身模式中唯一开启的插件，没有之一！结合`Shadowsocks`客户端可以实现科学上网，自定义多种上网模式，常用模式包括：

1. 直接连接 - 用于本地网络
2. 公司代理 - 通过代理访问大陆外网
3. Socks5 - 通过SS访问谷歌等GFW之外的网络

### ImageAssistant

图片助手，批量图片下载器，一款用于嗅探、分析网页图片并提供批量下载等功能及在线收藏、检索、分享服务的浏览器扩展程序。用的不多，给媳妇下载图片化PPT的时候有用到。

### 掘金

手机上装有掘金APP，对应的chrome 插件可用于获取技术资讯，类似于信息聚合工具，为程序员、设计师、产品经理每日发现优质内容，用的不多，目前禁用状态。

### 有道词典Chrome划词插件

支持Chrome浏览器的划词翻译，体验尚可，双击翻译，也可以听单词发音，一直在用，当然chrome自带的网页翻译功能也很强大，但是这个灵活一点，毕竟单词量在，少部分不懂的划词翻译还挺方便。

## 插件离线安装

1. 网络搜索对应的`.crx`插件文件
2. 使用解压软件解压.crx压缩文件
3. 在Chrome浏览器的扩展程序管理页面打开“开发者模式”
4. 选择“加载已解压的扩展程序”，然后选择对应的解压文件夹

在新版Chrome中，添加离线安装的插件后，每次都会弹框提示“请停用以开发者模式运行的扩展程序”，为了防止弹框，可以尝试以下方法:

ref: [彻底禁用Chrome的“请停用以开发者模式运行的扩展程序”提示](https://www.cnblogs.com/liuxianan/p/disable-chrome-extension-warning.html)

简言之，就是在Chrome的安装目录添加文件[version.dll](http://file.haoji.me/detail/27)

## 应用

### Wunderlist

奇妙清单的Chrome应用，单单这个插件就可以说是跨平台了。当然奇妙清单本身已基本支持全平台：

`Windows` `MAC OS` `Android` `IPhone` `Android Tablet` `IPAD` `WEB`

这也是我尝试大量清单软件后留存下来的，关键一点是公司网络不会将其屏蔽，所以通过它可以方便进行数据传输。

主要优点：

1. 全平台支持
2. 实时同步
3. 在Linux中使用Chrome应用也可以访问
4. 目前公司网络未能屏蔽
5. 相比于`todolist`免费版，奇妙清单更强大更良心
6. 支持团队协作，有用过该功能和同事进行bug追踪
7. 方便将文件从手机端同步至PC端

### Postman

这是一款功能强大的网页调试与发送网页请求的插件

## 配置页面

- 设置 chrome://settings/
- 扩展程序 chrome://extensions/
- 下载内容 chrome://downloads/
- 历史记录 chrome://history/
