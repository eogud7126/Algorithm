### 도시의 이름을 입력하면 그 도시의 날씨를 파싱하여 아두이노에 데이터를 보낸 후 반응한다.
```python
import urllib.request
import json
import serial

ser = serial.Serial(
port='COM11',
baudrate=9600,
)
while True:
    city=str(input("날씨를 알고싶은 도시의 이름을 영문으로 입력하세요.ex)Seoul: "))
    data=urllib.request.urlopen("http://api.openweathermap.org/data/2.5/weather?q="+city+"&APPID=*****************************")
    m=data.read()
    DB=json.loads(m)
    climate=DB["weather"]
    weather=climate[0]["main"]
    hot=DB["main"]
    temp=hot["temp"]-273.15
    print("\n"+city+"\n현재날씨:",weather,"\n현재 온도:",round(temp,2),"\n")

    if temp >= 30:
        op2="a"
    elif temp<30 and temp>=20:
        op2="b"
    elif temp<20 and temp>=10:
        op2="c"
    else :
        op2="d"
    
    
    if weather=="Clear":
        op1="r"
    elif weather=="Clouds":
        op1="y"
    elif weather=="Mist":
        op1="g"
    elif weather=="Rain" or weather=="Snow":
        op1="b"
    else :
        op1="o"

    ser.write(op1.encode())
    ser.write(op2.encode())

```
