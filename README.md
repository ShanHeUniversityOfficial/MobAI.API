# MobAI.API

## **使用方法**

### **使用流程总览**

1.申请密钥(https://api.shu.university/apply)
2.新建记录(https://api.shu.university/new)
3.循环聊天(https://api.shu.university/chat)
***other:[记录总览](https://api.shu.university/show)***

---

### **申请密钥**

#### **准备工作**
1.Python3.*
2.`pip install requests`

#### **示例代码**

```python
import requests
import sys

function = lambda json: sys.stdout.write(str(json))

function(
    requests.post(
        'http://api.shu.university/apply',
        json={
            'mail': 'demo@shu.university'
        }
    ).json()
)

```

#### **参数总览**

| 参数名 | 参数类型 | 是否必填 | 默认值 | 示例 |
| --- | --- | --- | --- | --- |
| mail | String | 是 | 无 | sb@xxx.com |

---

### **新建记录**

#### **准备工作**
1.Python3.*
2.`pip install requests`

#### **示例代码**

```python
import requests
import sys

function = lambda json: sys.stdout.write(str(json))

function(
    requests.post(
        'http://api.shu.university/new',
        json={
            'key': 'sk-demo',
            'model': 'MobAI'
        }
    ).json()
)

```

#### **参数总览**

| 参数名 | 参数类型 | 是否必填 | 默认值 | 示例 |
| --- | --- | --- | --- | --- |
| key | String | 是 | 无 | sk-demo |
| model | String | 是 | 无 | 天马行空 |

---

### **循环聊天**

#### **准备工作**
1.Python3.*
2.`pip install requests`

#### **示例代码**

```python
import requests
import sys

function = lambda data: sys.stdout.write(
    'MobAI:' + data.get('data').get('reply') + '\n\n'
    if data.get('state') == 'success'
    else 'ERROR:' + data.get('data').get('error') + '\n\n'
)

ask = input

while True:
    function(
        requests.post(
            url='http://api.shu.university/chat',
            json={
                'key': 'sk-demo',
                'id': 'id',
                'password': 'password',
                'question': ask('User:')
            }
        ).json()
    )

```

#### **参数总览**

| 参数名 | 参数类型 | 是否必填 | 默认值 | 示例 |
| --- | --- | --- | --- | --- |
| key | String | 是 | 无 | sk-demo |
| id | String | 是 | 无 | 0000-0000-0000-0000 |
| password | String | 是 | 无 | password-1234 |
| question | String | 是 | 无 | Hello! |


### 可参考示例

以下代码可直接运行，但不建议，因为这只是一个最基本的示例。

```python
import requests
import sys

ask = input
function = lambda data: sys.stdout.write(
    'MobAI:' + str(data.get('data').get('reply')) + '\n\n'
    if data.get('state') == 'success'
    else 'ERROR:' + data.get('data').get('error') + '\n\n'
)

requests.post(
    'http://api.shu.university/apply',
    json={'mail': ask('Mail:')}
)

key = ask('Key:')

ai = requests.post(
    'http://api.shu.university/new',
    json={
        'key': key,
        'model': 'ChatGPT4.0'
    }
).json()
function(ai)

while True:
    function(
        requests.post(
            url='http://api.shu.university/chat',
            json={
                'key': key,
                'id': ai.get('data').get('id'),
                'password': ai.get('data').get('password'),
                'question': ask('User:')
            }
        ).json()
    )

```
