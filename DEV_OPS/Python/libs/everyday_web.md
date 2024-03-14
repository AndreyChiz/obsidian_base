### GET-request_urllib
```python
import urllib.request  
import urllib.parse  
  
URL = 'http://localhost:8080'  
request_string = {'data': 'give_me_somth'}  
url_val = urllib.parse.urlencode(request_string)  
html=''  
  
request_url = f'{URL}?{url_val}'  
  
try:  
    with urllib.request.urlopen(request_url) as resp:  
        html = resp.read()  
  
except urllib.error.URLError as e:  
    print(e.reason)  
  
print(html)
```