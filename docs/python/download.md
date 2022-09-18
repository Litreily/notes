# Download

下载网络数据的几种方式，以下载图片为例

## urllib

```py
'''保存 url 对应数据到本地'''
urllib.request.urlretrieve(url, filename)
```

## requests

```py
'''保存 url 对应数据至 filepath 文件'''
res = requests.get(url, headers=headers, timeout=20)
with open(filepath, 'wb') as f:
    f.write(res.content)
```

或者使用下面的分块下载，这样可以下载**大文件**。

```py
res = requests.get(url, headers=headers, timeout=20)
with open(filepath, 'wb') as f:
    for chunk in res.iter_content(chunk_size=32):
        f.write(chunk)
```

不使用`with ... as`也可以，判断状态码为200后保存至文件。

```py
res = requests.get(url, headers=headers, timeout=20)
if res.status_code == 200:
    open(path, 'wb').write(res.content)
```

如果使用 `session` 的话，则稍加修改

```py
session = requests.Session()

# set session parameters like cookies and headers

res = session.get(url, timeout=20)
if res.status_code == 200:
    open(path, 'wb').write(res.content)
```

`requests`这4中方式大同小异，下载方式都是`requests.get` 或 `session.get`, 只是保存方式略有不同。

## scrapy

```py
'''在 pipelines.py 中 override get_media_requests'''
def get_media_requests(self, item, info):
    if isinstance(item, UrlItem):
        url = item['url']
        yield Request(url, meta={'item': item})
```

## telethon

在使用 `telethon` 下载 telegram 的媒体文件时，使用其API函数 `download_media` 即可。

```py
from telethon import TelegramClient, sync
from telethon.tl.types import InputMessagesFilterPhotos

'''set parameters'''
api_id = 123456
api_hash = 2349023481412
proxy = (socks.SOCKS5, "localhost", 1080)

tg_client = TelegramClient('tg_session', api_id=api_id,
                           api_hash=api_hash, proxy=proxy).start()

photos = tg_client.get_messages(
    'https://t.me/<channel>', None, filter=InputMessagesFilterPhotos)

for photo in photos:
    filename = os.path.join(os.path.expanduser('~'), 'photos',str(photo.id) + '.jpg')
    tg_client.download_media(photo, filename)
```
