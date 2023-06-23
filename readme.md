# cron, crontab
### 리눅스 작업 스케쥴러인 cron 에 대해 정리하는 곳
### cron 은 일정 시간마다 특정 명령어나 스크립트를 실행하게 만들어준다.
### demon 의 역할을 해준다.
### <br/><br/><br/>

## 스케줄 만들기 (crontab)
### 리눅스에서 crontab 은 처음에 nano editor 가 실행이 되는데 약간 불편하다.
### 그래서 select-editor 를 입력하여 vim 으로 바꿔준다.
#### ![image](https://github.com/Shin-jongwhan/cron/assets/62974484/7323ac64-24b7-4578-aa66-21905b6721ed)
### crontab 작업 등록은 -e 옵션을 써서 작성한다.
```
crontab -e
```
### 5 초마다 실행해준다.
#### ![image](https://github.com/Shin-jongwhan/cron/assets/62974484/3b6a328a-bbbd-4c07-8b31-106157969959)
### test code
```
sFile = "/home/jhshin/script/bi_system/cron_log_test.txt"
f = open(sFile, 'a')
f.write("test\n")
f.close()
```
### <br/>

### 작성된 작업 스케줄 확인
```
crontab -l
```
#### ![image](https://github.com/Shin-jongwhan/cron/assets/62974484/ac1f0aab-9165-4a9c-8a15-2acd5dd10ab2)
### <br/>

### 이제 test log 파일에 결과가 잘 입력되는지 봐보자
#### ![image](https://github.com/Shin-jongwhan/cron/assets/62974484/57c4c636-1a26-49a6-b0cb-3f895b7c413f)
