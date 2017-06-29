#AWS 생성 하기
1. 일단 가입부터
2. 지역 서울로 변경사용
3. AWS service 에서 우리가 사용할 EC2를 검색
	- EC2로 선택
4. Create Instance -> Lanuch Instance로 클릭
5. (step1.) OS 이미지 선택 -> Free tier eligible 아무거나 선택가능함 하지만 우리는 ubuntu를 사용 최신인 16.04 LTS를 사용한다
6. (step2.) 기본선택된것을 선택후 review and launch 선택
7. 계속해서 주욱 넥스트로 넘겨준다
8. (step.7) key pair를 생성해준다. 기존에잇을경우 기존것을 사용한다.
 - create a new ke...선택
 - key pair name 에 만들 key의 이름을 지정(나는 내 이니셜로 했음)
 - download key.. 해서 
 - ~/.ssh/아래에 옮겨준다.
 - .pem 권한이 -r--------(chmod 400 <name>.pem)변경
 - ubuntu 로 ubuntu는 작성을 한다
 - linux, suse ec2-userf로 작성
 - centos , centos로 작성
 - 우리는 우분투로 할예정이라 아래와 같이 작성
 - ```ssh -i ~/.ssh/ejjeong.pem ubuntu@ec2-13-124-135-143.ap-northeast-2.compute.amazonaws.com```
 - @이후 값은 aws에서 생성된 public dns값을 넣어준다
9. 접속을 하게되면 공개키값이 맞는지 물어보게된다
10. 이것을 확인을 위해 몇가지를 설치 해준다 
11. ```pip install awscli```를 설치 한다
 - 키값이 맞는지 확인하기위해서 설치해서 확인을 한다
 - aws 인터페이스를 터널에서 사용하기 위해
12. aws 연결을 위해 맨처음에만 입력한다
13. IAM 을 이용하여 User 생성
 - 생성할때 서비스에 iam검색 -> user 카테고리 이동
 - EC2-User 이름 지정 -> program...access선택 후 생성
 	- program..access 콘솔창에서 사용할수있는 유저
 	- Aws Ma...C...access aws콘솔창에서 사용할수잇는 유저 두가지중 선택 중복선택가능
 	- 유저가 만들어졌고 여기에 권한을 선택해서 넣어준다
 	- ec2를 검색해서 fullaccess를 선택
 	- accesskey ->
 	- scret access key ->
 	- region name -> ap-northeast-2
 	- default output -> json
 	확인은 ~/.aws에서 확인할수있다.
 	
13. ```aws configure```입력
 - 인스턴스 id 를 입력  
14. ```aws ec2 get-console-output --instance-id instance_id```으로 입력
15. 값만 확인
##AWS ubuntu에서 세팅
#### 언어팩 설치

```
sudo apt-get install language-pack-ko
sudo locale-gen ko_KR.UTF-8
```

## Ubuntu 기본 설정

#### python-pip설치

```
sudo apt-get install python-pip
```

#### zsh 설치

```
sudo apt-get install zsh
```


#### oh-my-zsh 설치

```
sudo curl -L http://install.ohmyz.sh | sh
```


#### Default shell 변경

```
sudo chsh ubuntu -s /usr/bin/zsh
```

#### pyenv requirements설치

[공식문서](https://github.com/yyuu/pyenv/wiki/Common-build-problems)

```
sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev \
libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils
```

#### pyenv 설치

```
curl -L https://raw.githubusercontent.com/yyuu/pyenv-installer/master/bin/pyenv-installer | bash
```

#### pyenv 설정 .zshrc에 기록

```
vi ~/.zshrc
export PATH="/home/ubuntu/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```


#### Pillow 라이브러리 설치

[공식문서](https://pillow.readthedocs.io/en/3.4.x/installation.html#basic-installation)

```
sudo apt-get install libtiff5-dev libjpeg8-dev zlib1g-dev \
    libfreetype6-dev liblcms2-dev libwebp-dev tcl8.6-dev tk8.6-dev python-tk
```



## Django 관련 설정

#### 장고 애플리케이션은 /srv Directory 사용
/ 아래에 srv 를 변경해준다(권한 변경)

```
sudo chown -R ubuntu:ubuntu /srv/
```


#사용 로컬에서 aws로 전송

