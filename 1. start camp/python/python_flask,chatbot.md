# 4일차

#### 터미널에 작성하는것들

flask_upgrade 폴더 생성

```python
$ mkdir flask_upgrade
```

폴더 이동

```python
$ cd flask_upgrade
```

서버켜기

```python
$ FLASK_app=app.py flask run --host=$IP --port=$PORT
```



로또 웹페이지 만들기

```python
@app.route('/lotto')
def lotto():
    return  render_template("lotto.html")
```



로또 6개 뽑기 코드

```python
from flask import Flask, render_template
import random
#improt random코드를 넣어주어야 코드가 돈다



app = Flask(__name__)
# 이게 있어야 하는데 왜일까....????? 지금은 이해하지 말자/.



@app.route('/lotto')
def lotto():
    num_list = range(1,46)
    pick = random.sample(num_list, 6)
    return  render_template("lotto.html", lotto=pick)
```





로또 결과 프로그램

**로또 결과 제공싸이트 주소**: **http://www.dhlottery.co.kr/common.do?method=getLottoNumber&drwNo=**



그후에 안전하지 않음으로 접속



chrome에서 json viewer 확장 파일 다운



```python
@app.route('/lotto')
def lotto():
    
    
    url = "https://www.dhlottery.co.kr/common.do?method=getLottoNumber&drwNo=837"
    #url추가
    
    
    num_list = range(1,46)
    pick = random.sample(num_list, 6)
    return  render_template("lotto.html", lotto=pick)
```





requests 다운을 위해서 터미널에



```$ pip install requests
$ pip install requests
```

그후

```pyth
import requests 
```

추가

```python
@app.route('/lotto')
def lotto():
    url = "https://www.dhlottery.co.kr/common.do?method=getLottoNumber&drwNo=837"
    res = requests.get(url)
    #res 추가
    
    num_list = range(1,46)
    pick = random.sample(num_list, 6)
    return  render_template("lotto.html", lotto=pick)
```



터미널에 python을 작성하면 python 코드를 사용가능하다.



print

type 등등 

나가는건 exit





두값에 비교해서 로또 당첨번호 비교하는 코드를 짜기

```python
from flask import Flask, render_template
import random
import requests
import json


app = Flask(__name__)


@app.route('/lotto')
def lotto():
    url = "https://www.dhlottery.co.kr/common.do?method=getLottoNumber&drwNo=837"
    res = requests.get(url).text
    lotto_dict = json.loads(res)
    print(lotto_dict["drwNoDate"])
    week_num = []
    week_format_num = []
    bonus = lotto_dict["bnusNo"]
    drwtNo = ["drwtNo1", "drwtNo2", "drwtNo3", "drwtNo4", "drwtNo5", "drwtNo6"]

    for num in drwtNo:
        number = lotto_dict[num]
        week_num.append(number)
        print(week_num)
        
    for i in range(1,7):
        num = lotto_dict["drwtNo{}".format(i)]
        week_format_num.append(num)
        
            
        
#num1 = lotto_dict["drwtNo1"]
#num2 = lotto_dict["drwtNo2"]
#num3 = lotto_dict["drwtNo3"]
#num4 = lotto_dict["drwtNo4"]
#num5 = lotto_dict["drwtNo5"]
#num6 = lotto_dict["drwtNo6"]
#bonum = lotto_dict["bnusNo"]
    
    
#print(lotto_dict["drwNoDate"])
#print(num1)
#print(num2)
#print(num3)
#print(num4)
#print(num5)
#print(num6)
#print(bonum)

    #pick = 우리가 생성한 번호
    #week_num = 이번주 당첨번호
    ##### 위의 두 값을 비교해서 로또 당첨 등수 출력!!!!!
    
    
    
    #print(type(res))
    #print(type(json.loads(res)))

    


    num_list = range(1,46)
    pick = random.sample(num_list, 6)
    pick.sort()
    
    
    lucky = 0
    for i in pick:
        if i in week_num:  
            lucky=lucky+1
            
            
    if lucky == 6:
        luck = "1등 입니다"
        
    elif lucky == 5:
        if bonus in pick:
            luck = "2등 입니다."
        else:
            luck = "3등 입니다."

    elif lucky == 4:
        luck = "4등 입니다."
        
    elif lucky == 3:
        luck = "5등 입니다."
    
    else:
        luck = "꽝입니다"
        
        
        
            
    
    #return  render_template("lotto.html", lotto=pick, num1=num1, num2=num2,  num3=num3,  num4=num4,  num5=num5, num6=num6,  bonum=bonum)
    return render_template("lotto.html",lotto=pick, week_num=week_num, week_format_num=week_format_num, luck=luck)
```



if 문 이용해서 1,3,4,5,6 등을 나누고



보너스 넘버를 기준으로 2,3, 등을 나눈다.



if 문 





선생님이 짜신 로또 확인 코드(짧은버전)



```python
@app.route('/lottery')
def lottery():
    # 로또 정보를 가져온다
    url = "https://www.dhlottery.co.kr/common.do?method=getLottoNumber&drwNo=837"
    res = requests.get(url).text
    lotto_dict = json.loads(res)
    
    # 1등 당첨 번호를 week 리스트에 넣는다.
    week = []
    for i in range(1,7):
        num = lotto_dict["drwtNo{}".format(i)]
        week.append(num)
    
    # 보너스 번호를 bonus 변수에 넣는다.
    bonus = lotto_dict["bnusNo"]
    
    # 임의의 로또 번호를 생성한다.
    pick = random.sample(range(1,46),6)

    # 비교해서 몇등인지 저장한다.
    match = len(set(pick) & set(week))
    
    if match==6:
        text = "1등"
    elif match==5:
        if bonus in pick:
            text = "2등"
        else:
            text = "3등"
    elif match==4:
        text = "4등"
    else:
        text = "꽝"
    
    # 사용자에게 데이터를 넘겨준다.
    
    return render_template("lottery.html",pick=pick, week=week,text=text)
```





핑퐁 작업



```python
@app.route('/ping')
def ping():
    return render_template("ping.html")
    
    
    
    
@app.route('/pong')
def pong():
    input_name = request.args.get('name')
    fake = Faker('ko_KR')
    fake_job = fake.job()
    #request 임. requests와 차이 기억!!!
    
    return render_template("pong.html", html_name=input_name, fake_job=fake_job)
```



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <form action="/pong">
        <input type="text" name="name"/>
        <input type="submit" value="Submit"/>
    </form>
</body>
</html>
```



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <a href="/ping">돌아가기</a>
    <h1>{{html_name}}님의 전생은 {{fake_job}} 입니다</h1>
</body>
</html>
```



딕셔너리 만드는거

```python
phonebook = {
    "치킨집":"02-000-0000",
    "피자집":"062-123-4567"
}




#가수 그룹의 딕셔너리를 만들어 주세요
#변수명 : 그룹이름
#key : 이름
#value : 나이(가상)


winner = {
    
    "강승윤":20,
    "송민호":21,
    "김진우":22,
    "이승훈":23
}


bts = {
    "RM":20,
    "슈가":21,
    "진":22,
    "제이홉":23
}




#변수명 : idol
#두개의 그룹을 넣어주세요

idol = {
    "winner":winner,
    "bts":bts   
}

#print(idol)
print(idol["bts"]["RM"])

score = {
        "수학":50,
        "국어":70,
        "영어":100
}

for key, value in score.items():
    print(key)
    print(value)
    
    
for key in score.keys():
    print(key)
    
    
    
for value in score.values():
    print(value)

#내가만든 sum 코드
s=0
for value in score.values():
        s = s + value
        
        print(s/3)
    
```





선생님이 만드신 sum 코드

```python
score_sum = 0
for value in score.values():
    score_sum = score_sum + value
    
print(score_sum/3)
```

# 챗봇 만들기

```python
import os
import requests
import json

token = os.getenv('TELE_TOKEN')
method = 'getUpdates'

url = "https://api.hphk.io/telegram/bot{}/{}".format(token,method)
print(url)
res = requests.get(url).json()


user_id = res["result"][0]["message"]["from"]["id"]


msg = "야"
method = 'sendMessage'

msg_url = "https://api.hphk.io/telegram/bot{}/{}?chat_id={}&text={}".format(token,method,user_id,msg)
print(msg_url)

requests.get(msg_url)




#print(res)
```

