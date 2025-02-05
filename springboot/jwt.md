# jwt 구성 요소
## 1. header
어떠한 알고리즘으로 암호화 할 것인지, 어떠한 토큰을 사용할 것 인지에 대한 정보가 들어 있음
## 2. payload
전달하려는 정보(claim)가 들어 있음
## 3. signature
**header**와 **payload**를 합친 후 지정한 **secret key**로 암호화 시켜 토큰을 변조하기 어렵게 만
