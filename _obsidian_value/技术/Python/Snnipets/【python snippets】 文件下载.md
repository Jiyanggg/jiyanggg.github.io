## Stream 流式下载

```
PROXIES = {
    "http": "http://192.168.1.50:1080",
}
file_path = 'file_path'
special_strings = ['\\', '/', ':', '：', '?', '？', '<', '>', '|', '*']
for special_string in special_strings:
    file_path = file_path.replace(special_string, ' ')

r = requests.get(file_url, stream=True, proxies=PROXIES)
with open(file_path, 'wb') as f:
    for chunk in r.iter_content(chunk_size=1024):
        f.write(chunk)
time.sleep(1)
```