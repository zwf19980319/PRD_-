# 项目名称：博物馆
# Product Requirement（产品说明文档）
| Title                     | Content |
| ------------------------- | ------- |
| Target release(发布日期)  | 2019/11 |
| Epic(史诗名称)            | 博物馆导览小程序  |
| Document status(文档状态) | 进行中  |
| Document owner(文件主人)  | 张玮锋  |
| Designer                 | 张玮锋  |

# Catalogue（目录）
- [PRD1加值宣言](#加值宣言)
- [PRD2核心价值](#核心价值)
- [PRD3核心价值与用户痛点](#核心价值与用户痛点)
- [PRD4人工智能概率性与用户痛点](#人工智能概率性与用户痛点)
- [PRD5需求列表与人工智能API加值](#需求列表与人工智能API加值)

# 产品定位
路线指引、展品查询、了解展品历史信息

# 加值宣言
### 核心
* 通用翻译API，支持28种语言实时互译，覆盖中、英、日、韩、西、法、泰、阿、俄、葡、德、意、荷、芬、丹等；同时支持28种语言的语言检测，提供基础文本翻译服务。
* 短语音识别API，将60秒以内的语音精准识别为文字，可适用于手机语音输入、智能语音交互、语音指令、语音搜索等短语音交互场景。
* 百度在线语音合成API，基于业界领先的深度神经网络技术，提供高度拟人、流畅自然的语音合成服务，让您的应用、设备开口说话，更具个性
* 高德地图室内定位API，高精度的定位体验
### 辅助
* （辅助）知识问答API对本产品价值部分在于：
基于海量数据，对用户需求进行深层次、知识化理解，并结合知识查询、推理、计算等多种技术，精准满足用户需求。为用户提供多领域、细粒度的知识问答服务。

# 核心价值  
* 语音合成：最小可用产品为能够实现有声读物功能。
* 语音识别：最小可用产品为能够准确识别博物馆管理员的介绍，将60s以内的语音精准识别为文字。

# 目标用户
以外国人为主要服务对象，外国人参加会展，可能没办法了解展区的展品信息，通过通用翻译功能，让他们了解具体信息。

# 用户痛点分析
# 人工智能概率性与用户痛点
* 语音合成：在多音字合成的时候发音不准确，不过对使用者的影响不太大。
* 通用翻译API：翻译内容可能没办法完全完善，不支持翻译很多。
* 百度AI人流量检测：如果任务重叠，可能检测不明确，较容易出现失误。
# 需求列表与人工智能API加值
| 用户案例                    | 对应API |重要程度|
| ------------------------- | ------- |---------|
|外国人前来参观博物馆,看不懂中文，需要翻译来观展 | 百度通用翻译API |极其重要|
|对于在观展的人们，由于人群过多，无法看到文字展示，可以用语音的方式来了解展览物件    | 百度AI语音合成api  |重要|
|当博物馆遇到人流量较大的时候，需要一个更加便捷的路线参观博物馆，给人们更方便的观展体验|百度AI人流量检测|重要|

# 原型
[原型文档]( http://nfunm171013102.gitee.io/museum_prototype)
# 原型文档
* 界面设计
![界面设计](https://images.gitee.com/uploads/images/2020/0109/152000_e0466c98_1648159.png "屏幕截图.png")
![功能](https://images.gitee.com/uploads/images/2020/0109/152052_128896a9_1648159.png "屏幕截图.png")
![人流量](https://images.gitee.com/uploads/images/2020/0109/152149_1d78a346_1648159.png "屏幕截图.png")
![语音](https://images.gitee.com/uploads/images/2020/0109/152223_0ae7c85d_1648159.png "屏幕截图.png")
# API产品使用关键AI或机器学习之API的输出入展示
## 使用水平
* 百度AI语音合成api：
``` python
import sys
import json

IS_PY3 = sys.version_info.major == 3
if IS_PY3:
    from urllib.request import urlopen
    from urllib.request import Request
    from urllib.error import URLError
    from urllib.parse import urlencode
    from urllib.parse import quote_plus
else:
    import urllib2
    from urllib import quote_plus
    from urllib2 import urlopen
    from urllib2 import Request
    from urllib2 import URLError
    from urllib import urlencode

API_KEY = 'zfNqZvwg7isWdaxGhrKLUoYb'
SECRET_KEY = '17ikGvyFdviAM53IvSkLBSbGSV638VGu'

TEXT = "Wu Ding, also known as Si Mu Wu Ding and Si Mu Wu Da Fang Ding, is a casting of the late Shang Dynasty (about the 14th century to the 11th century). It was unearthed in Wuguan "

# 发音人选择, 基础音库：0为度小美，1为度小宇，3为度逍遥，4为度丫丫，
# 精品音库：5为度小娇，103为度米朵，106为度博文，110为度小童，111为度小萌，默认为度小美 
PER = 4
# 语速，取值0-15，默认为5中语速
SPD = 5
# 音调，取值0-15，默认为5中语调
PIT = 5
# 音量，取值0-9，默认为5中音量
VOL = 5
# 下载的文件格式, 3：mp3(default) 4： pcm-16k 5： pcm-8k 6. wav
AUE = 3

FORMATS = {3: "mp3", 4: "pcm", 5: "pcm", 6: "wav"}
FORMAT = FORMATS[AUE]

CUID = "123456PYTHON"

TTS_URL = 'http://tsn.baidu.com/text2audio'


class DemoError(Exception):
    pass
"""  TOKEN start """

TOKEN_URL = 'http://openapi.baidu.com/oauth/2.0/token'
SCOPE = 'audio_tts_post'  # 有此scope表示有tts能力，没有请在网页里勾选


def fetch_token():
    print("fetch token begin")
    params = {'grant_type': 'client_credentials',
              'client_id': API_KEY,
              'client_secret': SECRET_KEY}
    post_data = urlencode(params)
    if (IS_PY3):
        post_data = post_data.encode('utf-8')
    req = Request(TOKEN_URL, post_data)
    try:
        f = urlopen(req, timeout=5)
        result_str = f.read()
    except URLError as err:
        print('token http response http code : ' + str(err.code))
        result_str = err.read()
    if (IS_PY3):
        result_str = result_str.decode()

    print(result_str)
    result = json.loads(result_str)
    print(result)
    if ('access_token' in result.keys() and 'scope' in result.keys()):
        if not SCOPE in result['scope'].split(' '):
            raise DemoError('scope is not correct')
        print('SUCCESS WITH TOKEN: %s ; EXPIRES IN SECONDS: %s' % (result['access_token'], result['expires_in']))
        return result['access_token']
    else:
        raise DemoError('MAYBE API_KEY or SECRET_KEY not correct: access_token or scope not found in token response')


"""  TOKEN end """

if __name__ == '__main__':
    token = fetch_token()
    tex = quote_plus(TEXT)  # 此处TEXT需要两次urlencode
    print(tex)
    params = {'tok': token, 'tex': tex, 'per': PER, 'spd': SPD, 'pit': PIT, 'vol': VOL, 'aue': AUE, 'cuid': CUID,
              'lan': 'zh', 'ctp': 1}  # lan ctp 固定参数

    data = urlencode(params)
    print('test on Web Browser' + TTS_URL + '?' + data)

    req = Request(TTS_URL, data.encode('utf-8'))
    has_error = False
    try:
        f = urlopen(req)
        result_str = f.read()

        headers = dict((name.lower(), value) for name, value in f.headers.items())

        has_error = ('content-type' not in headers.keys() or headers['content-type'].find('audio/') < 0)
    except  URLError as err:
        print('asr http response http code : ' + str(err.code))
        result_str = err.read()
        has_error = True

    save_file = "error.txt" if has_error else 'result.' + FORMAT
    with open(save_file, 'wb') as of:
        of.write(result_str)

    if has_error:
        if (IS_PY3):
            result_str = str(result_str, 'utf-8')
        print("tts api  error:" + result_str)

    print("result saved as :" + save_file)
    
```
* 输出结果
![输入图片说明](https://images.gitee.com/uploads/images/2019/1222/155122_94ae0e12_1648159.png "屏幕截图.png")

* 人流量检测代码
```
# encoding:utf-8

import requests
import base64

'''
人流量统计
'''

request_url = "https://aip.baidubce.com/rest/2.0/image-classify/v1/body_num"
# 二进制方式打开图片文件
f = open('很多人.jfif', 'rb')
img = base64.b64encode(f.read())

params = {"image":img}
access_token = '[24.b9cdc15b2954d18cd35a26778e38cc25.2592000.1579593802.282335-18083886]'
request_url = request_url + "?access_token=" + access_token
headers = {'content-type': 'application/x-www-form-urlencoded'}
response = requests.post(request_url, data=params, headers=headers)
if response:
    print (response.json())
 ```
 * 输出结果
 {'person_num': 16, 'log_id': 1311940341882461334}
 ![人流量](https://images.gitee.com/uploads/images/2019/1222/161049_e6906e65_1648159.png "屏幕截图.png")
 
 * 百度翻译API
 
 # 使用比较分析
||百度语音合成|阿里云语音合成|腾讯云语音合成|
|-|------|------|-------|
|准确度|60%|80%|0%|
|价格|较低，每日体验500次|较高，只有100次免费|* |
|成熟度|一般|较为成熟，拥有多款结合为一体的车型识别|* |
|性价比|较为高|较高|* |
|优点|可以识别大量的车的种类，并且会返回识别结果的相似度|相似度较高80%|* |
|缺点|遇到动物种类多的图片，不能都准确识别出动物的种类|只能识别出是什么车，而不能给出多种结果相似度对比||

* 翻译：

||百度通用翻译|阿里云通用翻译|腾讯云通用翻译|
|-|------|------|-------|
|准确度|60%|80%|0%|
|价格|较低，每日体验500次|较高，只有100次免费|* |
|成熟度|一般|较为成熟，拥有多款结合为一体的车型识别|* |
|性价比|较为高|较高|* |
|优点|可以识别大量的车的种类，并且会返回识别结果的相似度|相似度较高80%|* |
|缺点|遇到动物种类多的图片，不能都准确识别出动物的种类|只能识别出是什么车，而不能给出多种结果相似度对比||

* 人流量：

||百度云人流量检测|阿里云人流量检测|
|-|------|------|
|准确度|80%|70%|
|价格|较低|较高|
|成熟度|一般|较为成熟，拥有多种声音，多种形式|
|性价比|较为高|较高|
|优点|高精度头肩检测算法，准确率90%以上，静态人数统计不限人数，适应各种人群密集场所|流量识别，人群识别，统计图像中的人体个数，人流量，支持俯拍，正面，侧面等角度识别视角，无需正脸或全身照，识别没有人数上限，适应人群密集场景，可应用于：火车站，汽车站，景点入园口，会展中心，学校，机场，商场等密集场景。|
|缺点|当人脸模糊的时候，他检测会失败，或者会默认无人||

# 使用后风险报告
* 语音合成：
本产品的辅助API使用百度AI的语音合成功能，语音合成一篇481个字的儿童故事，需要105秒，发音准确，语调语速都可以满足幼年儿童的需求，同时用户可以根据自己的喜好选择发音人的语速语调声音。
* 语音识别：在说话人发音不标准的情况下，语音识别的准确率不高。 语音合成：对比了百度、讯飞、微软三家的产品后，三家公司在语音合成上的准确率都挺高，不过讯飞回应的速度是快于另外两家的。

# 加分项
* [百度翻译AI代码片段](https://gitee.com/NFUNM171013102/car_app_prototype/blob/master/code/%E7%99%BE%E5%BA%A6%E7%BF%BB%E8%AF%91AI)
* [百度语音合成AI代码片段](https://gitee.com/NFUNM171013102/car_app_prototype/blob/master/code/%E7%99%BE%E5%BA%A6%E8%AF%AD%E9%9F%B3%E5%90%88%E6%88%90)
* [百度人流量检测AI代码](https://gitee.com/NFUNM171013102/car_app_prototype/blob/master/code/%E4%BA%BA%E6%B5%81%E9%87%8F%E6%A3%80%E6%B5%8B%E4%BB%A3%E7%A0%81)
* [原型文档]( http://nfunm171013102.gitee.io/museum_prototype)  
###### 使用的API
* [百度人流量检测文档](https://ai.baidu.com/tech/body/num)
* [语音合成](https://ai.baidu.com/tech/speech/tts)

# 清单
* [百度翻译AI代码片段](https://gitee.com/NFUNM171013102/car_app_prototype/blob/master/code/%E7%99%BE%E5%BA%A6%E7%BF%BB%E8%AF%91AI)
* [百度语音合成AI代码片段](https://gitee.com/NFUNM171013102/car_app_prototype/blob/master/code/%E7%99%BE%E5%BA%A6%E8%AF%AD%E9%9F%B3%E5%90%88%E6%88%90)
* [百度人流量检测AI代码](https://gitee.com/NFUNM171013102/car_app_prototype/blob/master/code/%E4%BA%BA%E6%B5%81%E9%87%8F%E6%A3%80%E6%B5%8B%E4%BB%A3%E7%A0%81)
* [原型文档]( http://nfunm171013102.gitee.io/museum_prototype)  
###### 使用的API
* [百度人流量检测文档](https://ai.baidu.com/tech/body/num)
* [语音合成](https://ai.baidu.com/tech/speech/tts)
* [原型文档]( http://nfunm171013102.gitee.io/museum_prototype)

   
   
   
    
