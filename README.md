# 毕业纪念册

#### 产品定位：
1. 这个纪念册是为即将毕业的学生设计的，我们通常毕业了可能都有许多不舍，但当面无法说出口，这时我们可以通过实时语音输入，自动识别成文字，不仅能解放双手不需要手动打字，同时能在写留言的时候将文字填入同学录中。

2. 毕业后用户可以在纪念册中通过在地图上标记出自己学校的位置/学校内部的位置/其他位置，通过发布动态来写下自己的感受/发生过的趣事/与朋友经历过的事情等，使增加毕业后同学之间的沟通交流。

##### 核心价值：
用户在即将毕业时可以通过实时语音输入想要表达的话，既可以省去面对面说煽情话的尴尬，也不需要一个个字地打字。
用户通过在地图上自行标注定位发布一些往事或者目前生活，增加同学之间的沟通与联系。

#### 价值主张设计

#### PRD1 加值宣言：

- 百度开放平台API中实时语音录入价值：

通过实时语音录入，用户可以直接通过手机语音自动识别成文字，说话内容实时展示在屏幕上不需要手动敲打文字，解放双手。

- 高德地图API中的地理编码及静态地图结合

用户可以通过输入自己所在的位置，如中山大学南方学院，后会显示出静态地图，用户可以通过点击自定义的位置，然后发布自己的内容。

#### PRD2.核心价值

核心价值宣言（最小可用产品）：通过实时语音录入识别成文字，为用户填写同学录以及输入自己想说的话提供方便；通过用户自行输入内容故事，使用地图定位分享，增加毕业后同学们的沟通与交流，同时能够为自己日后回想起来自己的学生时代有媒介。

#### PRD3.核心价值与用户痛点

- 用户痛点

1. 我们以前写同学录都是使用纸质版的，不仅浪费树木资源，而且不易于保存，随着时间流逝，如果保存不当，纸质可能会发黄，发霉。

2. 电子版的同学录需要手动输入自己想表达的文字内容，较为麻烦

3. 目前的社交软件都是较为广泛地发布自己的生活内容，没有针对毕业生毕业纪念的模块，对用户纪念学生时代较为不方便。


#### PRD4.人工智能概率性与用户痛点

- AI概率性考量：

中国搜索引擎巨头百度表示，其新近研发的超级计算机Minwa在一项备受关注的人工智能基准测试ImageNet中取得了世界最好成绩，错误率仅为4.58%，超越了微软和谷歌的超级计算机。[百度超级计算机图像识别错误率创纪录 超越谷歌](https://tech.huanqiu.com/article/9CaKrnJL26x )

百度通过研究如何提高嘈杂环境下的英语语音识别准确率，收集了 9600 个人 7000 小时的语音样本，添加了 15 种噪声，把样本扩充到 10 万小时。吴恩达说这套系统的错误率比同期的微软 Bing Speech、Google Speech API 等竞争对手低 10%。[百度通过增加噪音样本降低错误率](https://www.huxiu.com/article/185744.html )



#### 需求列表与人工智能API加值 

|用户案例|对应API|重要程度|
|:-|:-:|-:|
|记录同学录时需要手动打字？|实时语音录入|重要|
|轻松定位发布故事|高德地图API|重要|

- 具体应用场景

1. 小明即将毕业了，同学找他写一些毕业寄语，小明拿出手机点击手机屏幕准备写的时候，同学提醒他说：“现在不用这么麻烦一个个字去打在下面啦，这个APP能够实时语音录入，你可以直接讲话，他就能识别成文字的”小明点击语音录入发现真的能够准确识别出来。

2. 小红参加毕业典礼时，拍了不少的照片，准备发朋友圈的时候，朋友看见了跟他说：“我用过一个APP无论你在哪里，都可以自行定位到任意一个地方就能发布动态，就算你在工作了，在想起母校时也能定位到这里。而且在那里都是毕业生的动态，发布自己在母校的趣事，等我们老了翻阅也更方便呀，现在的朋友圈都太杂了， 都是发布自己每天的动态生活，以后回看起来没有那么方便。”小红果断地下载了这个APP


#### API调用

### 1. 百度API语音识别API

- 输入

 ```
from aip import AipSpeech

""" 你的 APPID AK SK """
#宏定义
APP_ID = '18175774'
API_KEY = 'GQaQMLaIRjffPgeNNPWb****'
SECRET_KEY = '80gadDMUTsdFR4BRVvs0HvGvXEFo****' #由于隐私问题，我这个是随便填的一个数
                                               #你们要用自己的数据

client = AipSpeech(APP_ID, API_KEY, SECRET_KEY)

# 读取语音文件函数
def get_file_content(filePath):
    with open(filePath, 'rb') as fp:
        return fp.read()


# 识别本地文件  主函数
print(client.asr(get_file_content('C:\Users\Lenovo\Desktop\speaking.wav'), 'wav', 16000, {'dev_pid': 1536,}))

 ```
 
 - 输出
 
  ```
  
 {
    "err_no": 0,
    "err_msg": "success.",
    "corpus_no": "15984125203285357600",
    "sn": "235C524F-23TR-562F-73DR-9157WOMG3C8H",
    "result": ["网络与新媒体"]
}
 
 
 ```

2. 高德地图API调用

#####　地理编码

- 输入

 ```
 key_liu = 'a6e0d86bb5e96f5d29947b0da57*****'
def geo(add:str,city:str)-> dict:
    """获取地理编码"""
    url = 'https://restapi.amap.com/v3/geocode/geo?parameters'
    param = {
        'key':key_liu,
        'address':add,
        'city':city,
        'output':'json'
    }
    response = requests.get(url,params=param)
    data = response.json()
    return data

geo('广东省广州市从化区龙岗','广州')

 ```

- 输出

 ```
{'status': '1',
 'info': 'OK',
 'infocode': '10000',
 'count': '1',
 'geocodes': [{'formatted_address': '广东省广州市从化区龙岗',
   'country': '中国',
   'province': '广东省',
   'citycode': '020',
   'city': '广州市',
   'district': '从化区',
   'township': [],
   'neighborhood': {'name': [], 'type': []},
   'building': {'name': [], 'type': []},
   'adcode': '440117',
   'street': [],
   'number': [],
   'location': '113.668051,23.600869',
   'level': '热点商圈'}]}
   
  ```
    
 ##### ip定位
 
 - 输入

  ```
  key_liu = 'a6e0d86bb5e96f5d29947b0da57a*****'
def ip(ip:str)-> dict:
    """搜索ip"""
    url = 'https://restapi.amap.com/v3/ip?parameters'
    param = {
        'key':key_liu,
        'ip':ip,
       # 'types':types,
        'output':'json'
    }
    response = requests.get(url,params=param)
    data = response.json()
    return data
    
 ip('114.247.50.2')
   ```   
    
    
 - 输出
 
 ```  
 {'status': '1',
 'info': 'OK',
 'infocode': '10000',
 'province': '北京市',
 'city': '北京市',
 'adcode': '110000',
 'rectangle': '116.0119343,39.66127144;116.7829835,40.2164962'}

 ```  
    
