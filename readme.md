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
from datetime import datetime, timezone, timedelta


sDate_hms = datetime.now(timezone(timedelta(hours=9))).strftime('%Y%m%d%H%M%S')
sFile = "/home/jhshin/script/bi_system/cron_log_test.txt"
f = open(sFile, 'a')
f.write("test_{0}\n".format(sDate_hms))
f.close()
```
### <br/>

### 작성된 작업 스케줄 확인
```
crontab -l
```
#### ![image](https://github.com/Shin-jongwhan/cron/assets/62974484/5ce495fe-8ea5-42ff-942a-c562ff27f100)
### <br/>

### 이제 test log 파일에 결과가 잘 입력되는지 봐보자
#### ![image](https://github.com/Shin-jongwhan/cron/assets/62974484/7d62e9c5-d33e-40be-baa5-335e0b3992b7)
### <br/><br/><br/>

## ❗️ crontab 을 사용할 때 꼭 알아두어야 할 사항
### cron (crontab) 은 어떤 명령어를 실행할 때 최소한의 환경을 가지고 실행이 된다.
### 내가 현재 실행하고 있는 쉘의 환경으로 명령어가 실행되고 있다고 생각한다면, 에러를 맞이하게 될 것이다.
### 그래서 만약 자신이 접속하는 계정의 환경을 가져와서 사용하고 싶다면 몇 가지 고려해야 할 사항이 있다.
- python script 를 사용하고 싶다면 .sh 스크립트에서 실행하자.<br/>
ex)
  ```
  #!/bin/bash --login
  python test.py
  ```

- 나의 shell 환경을 가져오기 : .sh 의 맨 앞에 #!/bin/bash --login 을 붙이자
- 
- crontab 에서 내 PATH 를 가져오고 싶다면 다음과 같이 하자
  - PATH 확인<br/>
    ![image](https://github.com/Shin-jongwhan/cron/assets/62974484/ef7a720f-48be-407c-bcfa-aeb0940a69e3)
  - crontab -e 로 크론탭 등록에서 PATH 를 같이 명령어에 적어주기<br/>
    ![image](https://github.com/Shin-jongwhan/cron/assets/62974484/6e560aa0-8fed-4ccf-a1d6-abdc8ad5daec)
    
- conda 환경을 가져오고 싶다면 따로 init 을 해줘야 한다.<br/>
  ```
  # >>> conda initialize >>>
  # !! Contents within this block are managed by 'conda init' !!
  __conda_setup="$('/home/jhshin/miniconda3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
  if [ $? -eq 0 ]; then
      eval "$__conda_setup"
  else
      if [ -f "/home/jhshin/miniconda3/etc/profile.d/conda.sh" ]; then
          . "/home/jhshin/miniconda3/etc/profile.d/conda.sh"
      else
          export PATH="/home/jhshin/miniconda3/bin:$PATH"
      fi
  fi
  unset __conda_setup
  # <<< conda initialize <<<
  conda activate
  ```
  
- 자신의 ~/.bashrc 파일을 가져오고 싶을 때가 있는데 그럴 때는 '. ~/.bashrc' 를 쓰라고 한다. 앞에 '.' 은 source 를 대신한다고 한다. <br/>
  내가 이용하고 있는 환경은 우분투이고, 테스트해봤지만 적용되지 않았다.
  ```
  . ~/.bashrc
  ```
### <br/><br/><br/>



