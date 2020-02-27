# Hugo 블로그 생성, github.io 연결


1. 프레임워크 선정

2. Hugo 블로그 생성

  * hugo 설치
  
    `brew install hugo`
  
  * hugo 설치 확인 
  
    `hugo version`

  * hugo 사이트 자동생성
  
    `hugo new site <프로젝트명>`
    

3. github.io 

4. 쉘스크립트 생성

* 프로젝트 폴더로 이동

    `cd  ~/<프로젝트명>`
    
   
   * shell 스크립트 파일 생성
  
    `vi deploy.sh`


```
#!/bin/bash

echo -e "\033[0;32mDeploying updates to GitHub...\033[0m"

# Build the project. hugo -t <선택테마>
hugo -t hugo-theme-cleanwhite

# Go To Public folder
cd public
# Add changes to git.
git add .

# Commit changes.
msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin master

# Come Back up to the Project Root
cd ..


# blog 저장소 Commit & Push
git add .

msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"

git push origin master
```
 
   * 스크립트 실행을 위한 권한 설정
  
    `chmod +x deploy.sh`

   * shell 스크립트 실행
  
    `./deploy.sh`
