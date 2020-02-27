# Hugo 블로그 생성, github.io 연결


1. 프레임워크 선정

2. Hugo 블로그 생성

  * hugo 설치
  
    `brew install hugo`
  
  * hugo 설치 확인 
  
    `hugo version`

  * hugo 사이트 자동생성
  
    `hugo new site <프로젝트명>`

    `hugo new site blog`


  * 하기 사이트 에서 사용하고 싶은 hugo 테마 선택
  
   [Hugo theme](https://themes.gohugo.io/)
    
  * hugo 사이트 자동생성
  
    `git submodule add <테마.깃> themes/<테마명>`
    
    `git submodule add https://github.com/zhaohuabing/hugo-theme-cleanwhite.git themes/hugo-theme-cleanwhite`
    
  * hugo 테마 적용
  
    `hugo serve -t  <테마명>`
    
    `hugo serve -t  hugo-theme-cleanwhite`
    
    hugo **serve** -t <테마명> 여기서 "serve" 이 부분이 로컬에 웹서버를 띄워서 사이트를 생성하는 것.
    
  * hugo 테마 적용 확인
  
Built in 23 ms
Watching for changes in /Users/cathychae/blog/{archetypes,content,data,layouts,static,themes}
Watching for config changes in /Users/cathychae/blog/config.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)

    [hugo blog](http://localhost:1313/) 
    
    
  * 블로그 내용 저장소에 올리기
  
    `git remote add origin https://github.com/<유저아이디>/<프로젝트명>.git`
    -> 

    `git remote add origin https://github.com/EthanChaeSa/blog.git`
    
    
  * hugo 빌드하기 
  
    `hugo -t  <테마명>`

    `hugo -t  hugo-theme-cleanwhite`
    
    -> 빌드하고 나면 public 폴더가 생성됨
    -> 생성하고 나면 이 폴더를 깃에 올려야함
    
    
  * 빌드한 웹서버 깃에 올리기 
  
    `cd public`

    `git init`
    
    `cd ..`
    
    `git submodule add -b master <github 페이지> public`

    `git submodule add -b master https://github.com/EthanChaeSa/ethanchaesa.github.io.git public`
    
    `cd public`
    
    `git commit -m “initial commit"`
    
    `git push origin master`

   * 블로그 내용 깃에 올리기 완료
     
    cd ..
    
    git commit -m “initial commit"
    
    git push origin master
   
    
  
3. github.io 

4. 쉘스크립트 생성

* 프로젝트 폴더로 이동

    `cd  ~/<프로젝트명>`
    
* shell 스크립트 파일 생성

     `vi deploy.sh`
     
* 스크립트 실행을 위한 권한 설정

   `chmod +x deploy.sh`

* shell 스크립트 실행
  
    `./deploy.sh`



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



# Reference
https://github.com/Integerous/Integerous.github.io

https://ialy1595.github.io/post/blog-construct-1/

https://utteranc.es/

https://naraewool.gitbook.io/techwriter/today-i-learned/hugo


  
