---
layout: post
title:  "프로그래머가 youtube영상 받는법!"
date:   2017-03-04
excerpt: "youtube-dl과 쉘 스크립트로 동영상 다운받기."
tag:
- youtube-dl 
- shell script
- 유튜브 다운로드
---

**Youtube-dl 과 shell script 로 유튜브 동영상 자동으로 다운받는 스크립트 만들기**

youtube의 영상을 다운받는 방법은 매우 여러가지가 있습니다.



하지만 프로그래머, 소프트웨어엔지니어, 뭐라고 부르던, 코딩을 하는사람들은 youtube-dl 을 많이 씁니다.

 [youtube-dl 깃허브 주소 ](https://github.com/rg3/youtube-dl)

https://github.com/rg3/youtube-dl

뭘누르던 들어가집니다.

자세한 사용법은 영어로 쓰여있기 때문에 과감히 스킵 합니다.

~~영알못이라 인간적으로 옵션이 너무 많습니다.~~

그래서 우리는 딱 하나 youtube-dl의 기본옵션인 youtube-dl 명령어를 option없이 씁니다.



먼저 맥북 기준으로 터미널을 열어서

`pip3 install youtube-dl` 

을 해줍니다.

사실 리눅스도 똑같습니다. pip3 가 안깔려있는 노트북의 경우는 pip3 를 깔아줍니다.

pip3 는 파이썬 3 를 설치한뒤 깔면 됩니다. 가장 편한건 아나콘다 파이썬을 깔면 한방에 해결이 되죠 https://www.continuum.io/downloads 여기서 다운받으시면됩니다.



자 youtube-dl이 제대로 깔렸나 확인하기위해 커맨드라인에서 

`youtube-dl <youtube-url>`

을 쳐줍니다.

물론  <youtube-url>은 실제 동영상의 url을 넣어주면 됩니다.

 ~~<>이거 넣지마세요 ㅠㅠ~~

자 다운이 잘 됩니까?

안되면 …….스스로 해결해보는 능력을 기르는 좋은 기회가 될 것 같습니다..



그럼이제 shell script 를 배워봅시다.

```sh

\#!/bin/bash

echo "youtube downloader"
echo "paste folder name which will store videos"
read folder_name
echo "make sure your urls.txt file and this sh codes are at the same directory "
mkdir ./$folder_name
echo $(pwd) "this is your current directory"
echo "files will be downloaded at $(pwd)/$folder_name"
echo "default option is 'youtube-dl'"
echo "if you want to download in higher resolution" 
echo "plz change the shell script"
lines="../urls.txt"
cd $folder_name

while read line
do
​	youtube-dl --format mp4 $line
done<"$lines"

```


간단히 짜본 코드입니다.

한줄한줄 설명들어갑니다.

첫줄의 

`\#!/bin/bash`  는 이 코드가 쉘스크립트라는것을 알려줍니다.

`echo`는 사실상 그냥 print랑 같다고 보시면됩니다.

`read`는 python 의 input과 같은역할을 합니다.

변수를 받을때는  $없이, 변수를 사용할떄는 $와 함께 사용합니다.

`read folder_name`은 사용자로부터 입력을 받아서 그 문자열을 folder_name에 저장하는것입니다.

이 folder_name을 사용하고자 할 때는 $folder_name으로 꼭 $$$$$$$$$$이걸 붙여줘야합니다.

while문법은 조금 생소한 방법인데

while read line

do

​	blabla~~

done<"$lines"라고 되어있습니다.



 이는 lines에서 한줄씩 읽어오고 lines가 고갈될때까지 와일문을 돌린다는 이야기 입니다.

물론 blabla에는 와일문 한번씩  돌 때마다 할 내용을 지정해주면 됩니다.

위에 보면lines = "../urls.txt"로 urls.txt에 우리가 받고싶은 url주소를 한줄한줄 입력해 놓으면됩니다.

 youtube list로 된 비디오면 리스트가 주소에 포함된 url을 넣으면 한번에 리스트 전체가 받아집니다.


해당 스크립트는 urls.txt와 같은 디렉토리에 넣어주시면, 스크립트가 입력을 받아서 폴더생성해주고 그 폴더안에 urls.txt안에 들은 주소에 있는 영상을 다운받아줍니다.



