### AirtestIDE

#### Demo

```python
from airtest.core.api import *
from poco.drivers.android.uiautomation import AndroidUiautomationPoco

start_app('{package.name}')
poco=AndroidUiautomationPoco()
poco('android.widget.ImageView').click()

```

### Python

#### Demo

```text
airtest==1.0.27
pocoui==1.0.76
```

```python
from airtest.core.api import *
from poco.drivers.android.uiautomation import AndroidUiautomationPoco
auto_setup(__file__)
poco = AndroidUiautomationPoco()

auto_setup(__file__)
start_app("com.taobao.live")
poco = AndroidUiautomationPoco()
# poco('com.taobao.live:id/homepage2_search_btn').click()
poco('android.widget.ImageView').click()
poco('android.widget.ImageView').swipe([0.05, 0.01])
time.sleep(2)
anchor_name = poco('com.taobao.live:id/taolive_nickname_view').get_text()
poco('com.taobao.live:id/taolive_avatar_view').click()
poco('android.support.v7.widget.RecyclerView').child()
items = poco(type='android.view.View')

time.sleep(3)
for item in items:
    if '粉丝' in item.get_name():
        print(item.get_name(), anchor_name)
```

