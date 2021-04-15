---
layout: post
category: ubuntu 
---

# 문제

로컬에서는 잘 동작하던 미세먼지 조회 API가 서버에서는 잘 동작하지 않았다.

# 원인

미세먼지를 조회해오는 외부 API의 요청 결과를 확인하니 아래와 같았다.

```text
{"response":{"header":{"resultCode":"99","resultMsg":"해당 데이터 파일이 없습니다."}}}
```

이유는 미세먼지를 조회해오는 외부 API의 요청을 보낼때 시간을 같이 보내는데 서버 시간이 UTC 시간대를 사용하고 있었기 때문에 발생한 문제였다.

```bash
$ date
Thu Apr 15 01:49:49 UTC 2021
```

# 해결

대한민국 시간대(KST)를 사용하도록 설정한다.

## 시간대 변경 (tzselect)

```bash
$ tzselect
```

`tzselect` 명령어가 동작하지 않는다면, 아래 명령어로 설치한다.

```bash
$ apt install tzdata
```

<br>

`tzselect` 명령어를 입력하면 아래와 같은 화면이 나타난다. 

4를 입력한다.

```bash
Please identify a location so that time zone rules can be set correctly.
Please select a continent, ocean, "coord", or "TZ".
 1) Africa
 2) Americas
 3) Antarctica
 4) Asia
 5) Atlantic Ocean
 6) Australia
 7) Europe
 8) Indian Ocean
 9) Pacific Ocean
10) coord - I want to use geographical coordinates.
11) TZ - I want to specify the time zone using the Posix TZ format.
#? 4
```

23을 입력한다.

```bash
Please select a country whose clocks agree with yours.
 1) Afghanistan		  18) Israel		    35) Palestine
 2) Armenia		  19) Japan		    36) Philippines
 3) Azerbaijan		  20) Jordan		    37) Qatar
 4) Bahrain		  21) Kazakhstan	    38) Russia
 5) Bangladesh		  22) Korea (North)	    39) Saudi Arabia
 6) Bhutan		  23) Korea (South)	    40) Singapore
 7) Brunei		  24) Kuwait		    41) Sri Lanka
 8) Cambodia		  25) Kyrgyzstan	    42) Syria
 9) China		  26) Laos		    43) Taiwan
10) Cyprus		  27) Lebanon		    44) Tajikistan
11) East Timor		  28) Macau		    45) Thailand
12) Georgia		  29) Malaysia		    46) Turkmenistan
13) Hong Kong		  30) Mongolia		    47) United Arab Emirates
14) India		  31) Myanmar (Burma)	    48) Uzbekistan
15) Indonesia		  32) Nepal		    49) Vietnam
16) Iran		  33) Oman		    50) Yemen
17) Iraq		  34) Pakistan
#? 23
```

1을 입력한다.

```bash
The following information has been given:

	Korea (South)

Therefore TZ='Asia/Seoul' will be used.
Selected time is now:	Thu Apr 15 11:15:32 KST 2021.
Universal Time is now:	Thu Apr 15 02:15:32 UTC 2021.
Is the above information OK?
1) Yes
2) No
#? 1
```

<br>

아래와 같은 메시지가 나타난다면 설정이 완료되지 않은 것이다.
홈 디렉터리에 설정 파일에서 직접 시간대를 변경해야한다.

```bash
You can make this change permanent for yourself by appending the line
	TZ='Asia/Seoul'; export TZ
to the file '.profile' in your home directory; then log out and log in again.

Here is that TZ value again, this time on standard output so that you
can use the /usr/bin/tzselect command in shell scripts:
Asia/Seoul
```

## 시간대 변경 (.profile)

`cd -` 명령어를 통해 홈 디렉터리로 이동한다. `pwd` 명령어로 현재 위치를 확인한다.

```bash
$ cd -
$ pwd
/home/ubuntu
```

<br>

vi 편집기를 열어 직접 입력한다.

```bash
$ vi /home/ubuntu/.profile
```

```bash
TZ-'ASIA/SEOUL'; export TZ
```

# 참고

[https://gabii.tistory.com/entry/Ubuntu-한국-표준-시간KST-설정](https://gabii.tistory.com/entry/Ubuntu-%ED%95%9C%EA%B5%AD-%ED%91%9C%EC%A4%80-%EC%8B%9C%EA%B0%84KST-%EC%84%A4%EC%A0%95){:target="_blank"}

[https://emfls.tistory.com/entry/리눅스-터미널을-이용한-시스템-종료와-재부팅](https://emfls.tistory.com/entry/%EB%A6%AC%EB%88%85%EC%8A%A4-%ED%84%B0%EB%AF%B8%EB%84%90%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EC%8B%9C%EC%8A%A4%ED%85%9C-%EC%A2%85%EB%A3%8C%EC%99%80-%EC%9E%AC%EB%B6%80%ED%8C%85){:target="_blank"}